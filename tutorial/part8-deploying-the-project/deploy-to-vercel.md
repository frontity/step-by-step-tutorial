# Deploy to Vercel

Vercel is a cloud platform for static sites and Serverless Functions. It enables developers to host Node.js based projects simply and with minimal configuration required.

We highly recommend Vercel for hosting your Frontity site as it is serverless, cheap, includes a CDN, and is very easy to set up.

It also supports the cache technique `stale-while-revalidate` (they call it `Serverless Pre-Rendering`). This is a powerful way to improve your site speed.

### Create an account

In order to be able to deploy your site to Vercel you need to have an account. You can [signup here](https://vercel.com/signup) to create your Vercel account.

Once you have an account you [login](https://vercel.com/docs/cli#commands/login) to Vercel from the terminal.

```bash
> npx vercel login
```

After following their security process you will be logged in in your browser. Keep this browser tab open for the time being as we'll be referring to it later.

### Deploy your site

Before you can deploy your site to Vercel you will need to create a file called `vercel.json` in the root of your Frontity project. The file should contain the following code:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "package.json",
      "use": "@frontity/now"
    }
  ]
}
```

Once the file is created you can deploy your project from the command line using this command:

```bash
> npx vercel
```

You'll be asked a short series of questions about your project:

<p>
  <img alt="Deploying to Vercel" src="https://frontity.org/wp-content/uploads/2021/04/frontity-tutorial-part8img1.png">
</p>

Then, after a brief build process your deployed site will be ready. The address that you can use in your browser's address bar to reach the site will be displayed in the output from the command, and also in the Vercel console in your browser (which you kept open, didn't you?!).

For more information on deploying to Vercel, including how to use your own domain, see our "[Deploy to Vercel](https://docs.frontity.org/deployment)" documentation.
