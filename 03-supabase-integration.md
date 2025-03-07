# Supabase Integration

Learn how to integrate Supabase with your Lovable application for backend functionality.

## Overview

[Supabase](https://supabase.com/) is an open-source alternative to Firebase, offering real-time databases, authentication services, and file storage. It is built atop PostgreSQL, providing robust SQL querying capabilities and seamless integration with existing tools and frameworks. Supabase also features an intuitive web interface for effortless management of users and data.

## FAQ

**What is Supabase and how does it help Lovable users?**

Supabase is an open-source backend-as-a-service that provides authentication, databases (PostgreSQL), storage, and real-time capabilities. It helps Lovable users by handling data storage, authentication, and other backend functionalities without requiring manual setup.

**Do I need a separate subscription for Lovable and Supabase?**

Both Lovable and Supabase offer free tiers. However, if you need additional features, scalability, or more extensive use, you may need to subscribe to their paid plans separately.

**How do I connect Lovable with Supabase?**

1. In the Lovable editor, go to the **Integrations** section.
2. Click **Connect to Supabase** and follow the authentication steps.
3. If needed, create a new Supabase project within Lovable.
4. Lovable will automatically generate the necessary database schema and connect it to your project.

**How does Supabase handle scalability?**

Supabase uses **PostgreSQL**, one of the world's most scalable databases. It supports millions of rows and can handle high-traffic applications efficiently. Users on the **Pro Plan** or higher can access additional scaling features.

**How do I add real-time features like chat or live comments?**

Supabase provides **real-time capabilities** that Lovable can integrate with. You can:

* Add real-time listeners for comments or updates.
* Use **Supabase Storage** for image and file uploads.
* Enable live chat features in your app.

**Is there a limit to file uploads on Supabase?**

Supabase allows file uploads (images, videos, PDFs) with a **50MB limit on the free plan**. The **Pro Plan** supports resumable uploads for larger files.

**How do I configure authentication in Supabase?**

Lovable automatically sets up authentication, but you may need to:

* Go to **Supabase Dashboard > Authentication**.
* Enable **Email Sign-in/Sign-up**.
* Disable email confirmation for easier local testing.

## Supabase Setup

Connecting your Lovable app to Supabase is straightforward:

### Step 1: Create a Supabase account

Register a new Supabase account [here](https://app.supabase.com/sign-up) or [sign in](https://app.supabase.com/sign-in) if you already have one.

### Step 2: Create a new project in Supabase

Click on + New Project, complete the necessary fields, and allow a few minutes for setup.

### Step 3: Connect Supabase to Lovable

1. In your Lovable Editor, locate the Supabase button in the navbar. Click on it and select "Connect Supabase".
2. You will be redirected to a page where you will be able to select the relevant organisation.
3. You will be then redirected back to Lovable, where you will need to select the relevant project within that organisation.

After completing these steps, you will have to wait some seconds for your Supabase integration to finish. Look at the chat for this confirmation.

## Adding Authentication with Supabase

To initiate authentication, ensure that you have already connected Supabase project to your Lovable project.

To add a basic login page to your project, simply run a prompt similar to this:

```
Add login
```

You can then create a user by either:
* Creating a user directly via the Supabase Dashboard by navigating Supabase -> Authentication -> Users -> Add user.
* Signing up via the login page you've added

It's recommended to disable the email verification step for now, which you can do in Supabase -> Authentication -> Providers -> Email -> Disable "Confirm email".

## Storing Data with Supabase

Supabase offers a comprehensive Postgres database solution with tools that simplify database management. These include a table view that resembles a spreadsheet, capabilities to manage and replicate data relationships, a SQL editor, real-time database interactions, automated backups, and easy data import from CSV or Excel files.

To start building UI that uses your data stored in Supabase:

1. Ask Lovable to create a new feature and that you expect the data to be stored in Supabase.
2. Lovable will then provide you with a SQL snippet that you can run in the SQL editor in Supabase to create the table(s).
3. Once you confirm that you have run the SQL snippet, then Lovable will update the UI to allow you to interact with the data stored in Supabase.

## Storing Secrets with Supabase

If you are connected to Supabase, secret keys can be added to Lovable in two ways:

1. In the project settings.
2. In the chat if you ask it to show the secrets form.

These keys will be stored safely in Supabase's edge function secret manager and will be used when running Edge Functions, letting them connect to services as OpenAI, Stripe, Anthropic and more.

## Edge Functions

You can use Edge Functions to add powerful backend features like:

* Using AI to enhance your app's capabilities
* Sending emails to your users
* Processing payments
* Running scheduled tasks

Lovable will write and deploy Edge Functions to your Supabase project when implementing backend functionality.

When troubleshooting, you can visit the logs for your Edge Function in Supabase -> Functions -> Logs.

**Important Note**: Before you deploy your app to production or use any real data, you will need to review and set up the appropriate Row Level Security (RLS) policies. Lovable can help with that.
