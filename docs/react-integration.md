# GitForms + React Integration

> Add privacy-first contact forms to any React app.

## Quick Start

### 1. Install Dependencies

```bash
npm install @octokit/rest
# or
bun add @octokit/rest
```

### 2. Create GitForms Hook

```tsx
// hooks/useGitForms.ts
import { useState } from 'react';

interface SubmitOptions {
  name: string;
  email: string;
  message: string;
  labels?: string[];
}

export function useGitForms(config: {
  owner: string;
  repo: string;
  token: string;
}) {
  const [status, setStatus] = useState<'idle' | 'loading' | 'success' | 'error'>('idle');
  const [error, setError] = useState<string | null>(null);

  const submit = async ({ name, email, message, labels = ['contact'] }: SubmitOptions) => {
    setStatus('loading');
    setError(null);

    try {
      const response = await fetch(`https://api.github.com/repos/${config.owner}/${config.repo}/issues`, {
        method: 'POST',
        headers: {
          'Authorization': `Bearer ${config.token}`,
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          title: `Contact: ${name}`,
          body: `**From:** ${name}\n**Email:** ${email}\n\n**Message:**\n${message}`,
          labels
        })
      });

      if (!response.ok) throw new Error('Failed to submit');

      setStatus('success');
      return true;
    } catch (err) {
      setError(err instanceof Error ? err.message : 'Unknown error');
      setStatus('error');
      return false;
    }
  };

  return { submit, status, error, isLoading: status === 'loading' };
}
```

### 3. Create Form Component

```tsx
// components/ContactForm.tsx
import { useState } from 'react';
import { useGitForms } from '../hooks/useGitForms';

export function ContactForm() {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    message: ''
  });

  const { submit, status, isLoading } = useGitForms({
    owner: import.meta.env.VITE_GITFORMS_OWNER,
    repo: import.meta.env.VITE_GITFORMS_REPO,
    token: import.meta.env.VITE_GITHUB_TOKEN
  });

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    const success = await submit(formData);
    if (success) {
      setFormData({ name: '', email: '', message: '' });
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="Name"
        value={formData.name}
        onChange={(e) => setFormData({ ...formData, name: e.target.value })}
        required
      />
      <input
        type="email"
        placeholder="Email"
        value={formData.email}
        onChange={(e) => setFormData({ ...formData, email: e.target.value })}
        required
      />
      <textarea
        placeholder="Message"
        value={formData.message}
        onChange={(e) => setFormData({ ...formData, message: e.target.value })}
        required
      />
      <button type="submit" disabled={isLoading}>
        {isLoading ? 'Sending...' : 'Send'}
      </button>
      {status === 'success' && <p>Message sent!</p>}
      {status === 'error' && <p>Error. Please try again.</p>}
    </form>
  );
}
```

### 4. Environment Variables

```env
# .env
VITE_GITHUB_TOKEN=ghp_xxxxxxxxxxxx
VITE_GITFORMS_OWNER=your-username
VITE_GITFORMS_REPO=contact-submissions
```

## With Backend Proxy (Recommended for Production)

For production, never expose your GitHub token in the frontend. Use a backend proxy:

```tsx
// Backend proxy approach
const submit = async (data: SubmitOptions) => {
  const response = await fetch('/api/contact', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
  });
  return response.ok;
};
```

## With React Hook Form

```tsx
import { useForm } from 'react-hook-form';
import { useGitForms } from '../hooks/useGitForms';

interface FormData {
  name: string;
  email: string;
  message: string;
}

export function ContactForm() {
  const { register, handleSubmit, reset, formState: { errors } } = useForm<FormData>();
  const { submit, status, isLoading } = useGitForms({
    owner: 'your-username',
    repo: 'contact-submissions',
    token: 'your-token'
  });

  const onSubmit = async (data: FormData) => {
    const success = await submit(data);
    if (success) reset();
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register('name', { required: true })} placeholder="Name" />
      {errors.name && <span>Name is required</span>}

      <input {...register('email', { required: true, pattern: /^\S+@\S+$/i })} placeholder="Email" />
      {errors.email && <span>Valid email required</span>}

      <textarea {...register('message', { required: true })} placeholder="Message" />
      {errors.message && <span>Message is required</span>}

      <button type="submit" disabled={isLoading}>
        {isLoading ? 'Sending...' : 'Send'}
      </button>
    </form>
  );
}
```

## Benefits

- **Zero tracking** - No analytics, no cookies
- **Your data** - Stored in YOUR GitHub repo
- **Free forever** - No limits, no tiers
- **Framework agnostic** - Works with any React setup

---

**[Back to GitForms](../README.md)**
