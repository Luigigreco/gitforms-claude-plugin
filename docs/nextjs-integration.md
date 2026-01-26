# GitForms + Next.js Integration

> Add privacy-first contact forms to your Next.js app in minutes.

## Quick Start

### 1. Install GitForms MCP Server

```bash
npm install @gitforms/mcp-server
# or
bun add @gitforms/mcp-server
```

### 2. Create Form Component

```tsx
// components/ContactForm.tsx
'use client';

import { useState } from 'react';

interface FormData {
  name: string;
  email: string;
  message: string;
}

export default function ContactForm() {
  const [formData, setFormData] = useState<FormData>({
    name: '',
    email: '',
    message: ''
  });
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
    <form onSubmit={handleSubmit} className="space-y-4">
      <input
        type="text"
        name="name"
        placeholder="Your Name"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
        required
        className="w-full p-2 border rounded"
      />
      <input
        type="email"
        name="email"
        placeholder="Your Email"
        value={formData.email}
        onChange={(e) => setFormData({ ...formData, email: e.target.value })}
        required
        className="w-full p-2 border rounded"
      />
      <textarea
        name="message"
        placeholder="Your Message"
        value={formData.message}
        onChange={(e) => setFormData({ ...formData, message: e.target.value })}
        required
        className="w-full p-2 border rounded h-32"
      />
      <button
        type="submit"
        disabled={status === 'loading'}
        className="w-full p-2 bg-blue-500 text-white rounded hover:bg-blue-600 disabled:opacity-50"
      >
        {status === 'loading' ? 'Sending...' : 'Send Message'}
      </button>
      {status === 'success' && <p className="text-green-600">Message sent!</p>}
      {status === 'error' && <p className="text-red-600">Failed to send. Try again.</p>}
    </form>
  );
}
```

### 3. Create API Route

```ts
// app/api/contact/route.ts
import { NextResponse } from 'next/server';
import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: process.env.GITHUB_TOKEN });

export async function POST(request: Request) {
  try {
    const { name, email, message } = await request.json();

    // Create GitHub Issue as form submission
    await octokit.issues.create({
      owner: process.env.GITFORMS_OWNER!,
      repo: process.env.GITFORMS_REPO!,
      title: `Contact: ${name}`,
      body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
      labels: ['contact', 'gitforms']
    });

    return NextResponse.json({ success: true });
  } catch (error) {
    console.error('GitForms error:', error);
    return NextResponse.json({ error: 'Failed to submit' }, { status: 500 });
  }
}
```

### 4. Environment Variables

```env
# .env.local
GITHUB_TOKEN=ghp_xxxxxxxxxxxx
GITFORMS_OWNER=your-username
GITFORMS_REPO=contact-submissions
```

## App Router vs Pages Router

### App Router (Next.js 13+)
Use the example above with `app/api/contact/route.ts`

### Pages Router
```ts
// pages/api/contact.ts
import type { NextApiRequest, NextApiResponse } from 'next';
import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: process.env.GITHUB_TOKEN });

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse
) {
  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Method not allowed' });
  }

  const { name, email, message } = req.body;

  try {
    await octokit.issues.create({
      owner: process.env.GITFORMS_OWNER!,
      repo: process.env.GITFORMS_REPO!,
      title: `Contact: ${name}`,
      body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
      labels: ['contact', 'gitforms']
    });

    res.status(200).json({ success: true });
  } catch (error) {
    res.status(500).json({ error: 'Failed to submit' });
  }
}
```

## With Server Actions (Next.js 14+)

```tsx
// app/contact/actions.ts
'use server';

import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: process.env.GITHUB_TOKEN });

export async function submitContact(formData: FormData) {
  const name = formData.get('name') as string;
  const email = formData.get('email') as string;
  const message = formData.get('message') as string;

  await octokit.issues.create({
    owner: process.env.GITFORMS_OWNER!,
    repo: process.env.GITFORMS_REPO!,
    title: `Contact: ${name}`,
    body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
    labels: ['contact', 'gitforms']
  });

  return { success: true };
}
```

## Benefits

- **Zero tracking** - No analytics, no cookies
- **Your data** - Stored in YOUR GitHub repo
- **Free forever** - No limits, no tiers
- **Type-safe** - Full TypeScript support

---

**[Back to GitForms](../README.md)**
