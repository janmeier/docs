# Vercel Postgres

Snaplet is a powerful tool for capturing a subset of your PostgreSQL database and transforming the data using TypeScript. With Snaplet, you can easily create a snapshot of your production data and restore it in a development or staging environment, without compromising sensitive information. This allows you to work with realistic data and test your applications in a safe and controlled manner.

One of the key benefits of Snaplet is that it is fully customizable using TypeScript. You can write TypeScript code to manipulate the data in the snapshot, such as filtering, aggregating, or anonymizing it. This makes Snaplet a flexible and versatile tool that can adapt to your specific needs.

In this tutorial, we will show you how to use Snaplet to capture a snapshot of your production database, and how to restore it in Vercel Postgres. Vercel Postgres is a fully managed PostgreSQL database service that offers high performance, scalability, and security. By combining Snaplet and Vercel Postgres, you can easily move your data between environments and accelerate your development process.

## Overview

In this tutorial, we will show you how to capture a snapshot of your PostgreSQL database using Snaplet, and how to restore it in Vercel Postgres. The process involves four main steps:

    1. Capture a snapshot via Snaplet.
    2. Create a Vercel Postgres database.
    3. Install the Snaplet CLI.
    4. Restore the snapshot into Vercel.

By following these four steps, you will be able to easily move your data between environments and speed up your development process. Let's get started!


## Capture a snapshot

Snaplet offers two deployment options: you can use the cloud tool, which is a fully managed service provided by Snaplet, or you can self-host Snaplet on your own infrastructure.

We will focus on using the cloud tool provided by Snaplet. This is a great option if you want to get started quickly without having to set up your own infrastructure. However, if you have specific requirements or constraints that make self-hosting a better option for you, we encourage you to explore that option as well.

The Snaplet onboarding process is faily automatic, follow the prompts and wait for your first snapshot.

<div style={{"position":"relative","paddingBottom":"64.98194945848375%","height":"0"}}><iframe src="https://www.loom.com/embed/26f6aae49d8b425fb31358664d17e8a6" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style={{"position":"absolute","top":"0","left":"0","width":"100%","height":"100%"}}></iframe></div>


## Create a Vercel Postgres database

Head on over to your Vercel dashboard, select the "Storage" tab, and follow the prompts to create a Postgres database.

<div style={{"position":"relative","paddingBottom":"64.98194945848375%","height":"0"}}><iframe src="https://www.loom.com/embed/86b290abdaaf444d85c592dce24ae6ce" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style={{"position":"absolute","top":"0","left":"0","width":"100%","height":"100%"}}></iframe></div>

## Install and configure Snaplet CLI

Snaplet works as a companion to your codebase. When you install it for yourself, you install it for all members of your team. So head on over to your codebase and add it as a dependency.

```terminal
npm install --dev snaplet
```

Next, you'll need to associate your CLI to your Snaplet account, and select the project where your snapshots are stored.


```terminal
npx snaplet setup
```

<div style={{"position":"relative","paddingBottom":"64.98194945848375%","height":"0"}}><iframe src="https://www.loom.com/embed/c7210f5c54b84d028d14a6c15183e20f" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style={{"position":"absolute","top":"0","left":"0","width":"100%","height":"100%"}}></iframe></div>

## Restore the snapshots into Vercel

Now that you have captured a snapshot using Snaplet and created a Vercel Postgres database, you can restore the snapshot into Vercel using the following steps:

```terminal
npx snaplet snapshot restore
```

<div style={{"position":"relative","paddingBottom":"64.98194945848375%","height":"0"}}><iframe src="https://www.loom.com/embed/786ed55ea98c4124baeedc88191cead9" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style={{"position":"absolute","top":"0","left":"0","width":"100%","height":"100%"}}></iframe></div>

## Conclusion

In conclusion, Snaplet is a powerful tool that can help you move your PostgreSQL data between environments and speed up your development process. By capturing a snapshot of your production database and transforming it using TypeScript, you can work with realistic data without compromising sensitive information. And by restoring the snapshot into Vercel Postgres, you can benefit from a fully managed, high-performance database service that scales with your application.

We hope that this guide has been helpful and that you are now ready to use Snaplet to streamline your database management process. If you have any questions or feedback, please don't hesitate to reach out to us. Thanks for reading!