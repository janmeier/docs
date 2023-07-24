# Supabase Clone Environments

This guide will help you get a development Supabase instance set up using Snaplet. In 15 minutes or less, you will create a snapshot of your production Supabase instance and restore it to a development environment you can safely code against.

:::note
**Note:** We’ve spent a lot of time ensuring that Snaplet works seamlessly with Supabase, however, if you experience any issues with getting Supabase working with Snaplet, or with this guide, feel free to come chat with us on [Discord](https://app.snaplet.dev/chat).
:::

## Clone Supabase production data, without sensitive information, to a development environment

We’re massive fans of Supabase because it makes it so easy to start a project with a dedicated PostgreSQL database. However, we’re willing to bet you know the pain and manual configuration in setting up multiple environments on Supabase and populating each of those with data - that’s why you’re here after all!

Fortunately, Snaplet makes populating your multiple development environments with data and keeping that data consistent across those environments, incredibly simple. This is rooted in a philosophy we believe in here at Snaplet: [Environment parity](https://www.oreilly.com/content/environment-parity-for-rapidly-deployed-cloud-native-apps/).

Environment parity sounds like a dream come true. In this guide, we’re going to tell you exactly how to do that with your data in Supabase! End-to-end, it shouldn’t take more than 15 minutes, and doing so will allow you to code against an accurate development environment that you can sync with production.

<div style={{textAlign: 'center'}}>

![I absolutely love Supabase!](/img/snappy-holding-supabase-logo.svg)

</div>

### Things you'll need before you begin:

1. **A production Supabase project’s connection string:** This can be found in Supabase via Organization > All Projects > Your Project > Project Settings > Connection Pooling > Connection String. We’ll refer to this in the guide as your “source database” - where your data comes from.

<img src="/screenshots/supabase_connection_string.webp" alt="Snaplet onboarding select team name" style={{ border: "1px solid #e5e7eb" }} />

2. **A development Supabase project’s connection string:** Same steps as above, but a different project/environment. We’ll refer to this in the guide as your “target database” - where we’re restoring the snapshot of the source database to. If you haven’t got this set up yet, we’ll take you through the process of setting this up.

> **Highly Recommended:** Create a read-only role for your connection string. For more info on how to create a read-only role across all schemas, you can check out [our docs](/guides/postgresql#create-a-read-only-role).

### Step 1: Connect your source database (Production Database)

The first thing you’ll want to do is navigate to https://www.snaplet.dev/ and sign up for a new account (it’s free). Once you have successfully signed up for a new account, you’ll begin the onboarding process...

<img src="/screenshots/onboarding_start.webp" alt="Snaplet onboarding select team name" style={{ border: "1px solid #e5e7eb" }} />

On the “Connect database” step add your Supabase production database (using your read-only role). This is the source database we defined above.

<img src="/screenshots/checking_creds.png" alt="Snaplet onboarding connect your database" style={{ border: "1px solid #e5e7eb" }} />

### Step 2: Create a snapshot

Once that is done, continue to the next steps:

- Subsetting (skipping will create a snapshot with all your data).
- Transforming (skipping will leave all your table columns untouched).

Once you have gone through those steps, a new snapshot process will start and you will now be on the “capture step.” Wait for it to finish - this is the snapshot you will restore into your **target database.**

<img src="/screenshots/onboarding_capture.webp" alt="Snaplet onboarding capturing your database" style={{ border: "1px solid #e5e7eb" }} />

### Step 3: Create a target database on Supabase (Development Database)

Your target database is where you want Snaplet to restore the captured snapshot of your production project. This would most likely be either your staging or developer Supabase project.

If you don’t already have a developer database setup on Supabase, you’ll need to create a new database by setting up a new project on Supabase. To create a new project you’ll have to do the following:

1. Go to [app.supabase.io](https://app.supabase.io/)
2. Go to your organization > All projects
3. In the top left click on your current project name and **new project**

   ![Connection string uri in supabase](/screenshots/supabase-integration/new_project.png)

4. Wait for the new database to launch

> Remember the password you use when creating the project. You’ll need this password to connect your database to Snaplet later.

### Step 4: Install the Snaplet CLI

1. Open your terminal and run `curl -sL https://app.snaplet.dev/get-cli/ | bash`
2. Run `snaplet auth login`
3. Navigate to `https://app.snaplet.dev/access-token/cli` to get your access token.
4. Paste the access token in the terminal.

### Step 5: Config setup

You're now ready to restore your production snapshot into your Supabase development project.

1. Navigate to your project directory
2. Run `snaplet config setup`

   1. You will be shown a warning to write create `.snaplet/config` in your project directory. Select yes (y) to create the file.
   2. Then you will be asked for a **target database connection string.** These are the database credentials of your **target database that we set up in step 3** (your staging or development database).

   > Note that you need to be using the `postgres` user for your development environment

3. Run `snaplet project setup` - you will be presented with a list of projects, these are databases that are connected to your Snaplet account. Choose the project that contains the snapshot you created in step 2.

### Step 6: Restore the data target

With all the above steps complete, we can now restore!

1. Run `snaplet snapshot restore --no-reset`

> **Note on `--no-reset`:** This will skip the “reset” step of the restore command. So no existing schemas will be dropped. Learn more about data operations [here](/getting-started/restoring#opting-out)

<div style={{textAlign: 'center'}}>

![Supabase is fun!](/img/snappy-with-supabase-ball.svg)

</div>

## All done!

If you want to learn more about Snaplet, you can explore our docs. If you have any questions, feel free to reach out on [Discord](https://app.snaplet.dev/chat).

That’s it! You’re all done, and should have restored a version of your Supabase production database with transformed data into your target database. You can now safely code against production-realistic data.

## Supabase local development

Supabase allows you [develop locally](https://supabase.com/docs/guides/cli/local-development) through their CLI, you can easily restore any snapshot created in Snaplet to your local instance, just by running:

```bash
# Login in to the Supabase CLI
supabase login

# Initialize Supabase to set up the configuration for developing your project locally:
supabase init

# With docker installed and running start up your supabase services locally
supabase start

# Grab the local database url and insert into the ./snaplet/config.json file
# Restore to the target database url
snaplet ss r --no-reset
```

## Troubleshooting

### Warnings after restoring

When running the restore command, you may see warnings such as:

```jsx
Could not drop schema "auth", Snaplet will try to truncate all tables and related objects as a fallback: error: must be owner of schema auth
[Schema] Warning: type "aal_level" already exists, statement: "CREATE TYPE auth.aal_level AS ENUM (...
```

Supabase includes a few schemas that are not owned by the `postgres` user, for example: **auth**, **graphql**, **realtime,** and **storage.** During the capture process, Snaplet will try to capture data for tables under these schemas (if it has permission to read data from them)

Your **target database** may already contain these schemas when restoring. The warnings just mean that when Snaplet attempted to restore these schemas (**auth, graphql**, etc) but was unable to drop the ones already existing in your **target database** (since the user is not an owner of these), and consequently it was not able to create any structure for them (since that structure still exists)

Snaplet will still make sure to clear all data for tables in these schemas and restore data for each of these tables to what is in the snapshot. In other words, **these warnings do not mean that the restore failed, but rather show you what Snaplet tried to do.**

If you aren't actually needing the data for some of these schemas, you can stop these warnings by excluding the schema from the captured snapshots. You can read more on how to do this [over here in our docs](https://docs.snaplet.dev/references/data-operations/exclude):

![Example of excluding a schema](/img/snaplet-supabase-schema-exclude.png)

---
