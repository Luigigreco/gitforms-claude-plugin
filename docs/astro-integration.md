# GitForms + Astro Integration

> Add privacy-first contact forms to your Astro site.

## Quick Start

### 1. Install Dependencies

```bash
npm install @octokit/rest
# or
bun add @octokit/rest
```

### 2. Create API Endpoint

```ts
// src/pages/api/contact.ts
import type { APIRoute } from 'astro';
import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: import.meta.env.GITHUB_TOKEN });

export const POST: APIRoute = async ({ request }) => {
  try {
    const data = await request.json();
    const { name, email, message } = data;

    await octokit.issues.create({
      owner: import.meta.env.GITFORMS_OWNER,
      repo: import.meta.env.GITFORMS_REPO,
      title: `Contact: ${name}`,
      body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
      labels: ['contact', 'gitforms']
    });

    return new Response(JSON.stringify({ success: true }), {
      status: 200,
      headers: { 'Content-Type': 'application/json' }
    });
  } catch (error) {
    return new Response(JSON.stringify({ error: 'Failed to submit' }), {
      status: 500,
      headers: { 'Content-Type': 'application/json' }
    });
  }
};
```

### 3. Create Form Component

```astro
---
// src/components/ContactForm.astro
---

<form id="contact-form" class="space-y-4">
  <input
    type="text"
    name="name"
    placeholder="Your Name"
    required
    class="w-full p-2 border rounded"
  />
  <input
    type="email"
    name="email"
    placeholder="Your Email"
    required
    class="w-full p-2 border rounded"
  />
  <textarea
    name="message"
    placeholder="Your Message"
    required
    class="w-full p-2 border rounded h-32"
  ></textarea>
  <button
    type="submit"
    class="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600"
  >
    Send Message
  </button>
  <p id="status" class="hidden"></p>
</form>

<script>
  const form = document.getElementById('contact-form') as HTMLFormElement;
  const status = document.getElementById('status') as HTMLParagraphElement;

  form.addEventListener('submit', async (e) => {
    e.preventDefault();

    const formData = new FormData(form);
    const data = Object.fromEntries(formData);

    try {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
      });

      if (response.ok) {
        status.textContent = 'Message sent successfully!';
        status.className = 'text-green-600';
        form.reset();
      } else {
        throw new Error('Failed');
      }
    } catch {
      status.textContent = 'Failed to send. Please try again.';
      status.className = 'text-red-600';
    }

    status.classList.remove('hidden');
  });
</script>
```

### 4. Use in Page

```astro
---
// src/pages/contact.astro
import Layout from '../layouts/Layout.astro';
import ContactForm from '../components/ContactForm.astro';
---

<Layout title="Contact Us">
  <main class="max-w-md mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Contact Us</h1>
    <ContactForm />
  </main>
</Layout>
```

### 5. Environment Variables

```env
# .env
GITHUB_TOKEN=ghp_xxxxxxxxxxxx
GITFORMS_OWNER=your-username
GITFORMS_REPO=contact-submissions
```

## With React Island

If you prefer React components in Astro:

```tsx
// src/components/ContactForm.tsx
import { useState } from 'react';

export default function ContactForm() {
  const [formData, setFormData] = useState({ name: '', email: '', message: '' });
  const [status, setStatus] = useState<'idle' | 'loading' | 'success' | 'error'>('idle');

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setStatus('loading');

    try {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(formData)
      });

      if (response.ok) {
        setStatus('success');
        setFormData({ name: '', email: '', message: '' });
      } else {
        setStatus('error');
      }
    } catch {
      setStatus('error');
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* Form fields... */}
    </form>
  );
}
```

```astro
---
// src/pages/contact.astro
import ContactForm from '../components/ContactForm';
---

<ContactForm client:load />
```

## Static Site with Actions

For fully static sites, use Astro Actions (Astro 4.15+):

```ts
// src/actions/index.ts
import { defineAction } from 'astro:actions';
import { z } from 'astro:schema';
import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: import.meta.env.GITHUB_TOKEN });

export const server = {
  submitContact: defineAction({
    input: z.object({
      name: z.string(),
      email: z.string().email(),
      message: z.string()
    }),
    handler: async ({ name, email, message }) => {
      await octokit.issues.create({
        owner: import.meta.env.GITFORMS_OWNER,
        repo: import.meta.env.GITFORMS_REPO,
        title: `Contact: ${name}`,
        body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
        labels: ['contact', 'gitforms']
      });
      return { success: true };
    }
  })
};
```

## Benefits

- **Zero tracking** - No analytics, no cookies
- **Your data** - Stored in YOUR GitHub repo
- **Free forever** - No limits, no tiers
- **SSR or Static** - Works with any Astro mode

---

**[Back to GitForms](../README.md)**
