# Deploying the project

Web development projects can rarely be considered complete and there is quite often additional work that needs doing even after deployment. It is also usual for web projects to change and evolve over time and/or require ongoing maintenance and further development.

However, for our current purposes we can at this point consider our application finished and ready to deploy.

We can create a production version of our project by running the following command from the root of your project:

```bash
> npx frontity build
```

This command will generate a `build` directory containing both your (isomorphic) React app and your Frontity (Node.js) server. You can then run the following command to serve the site from your local Node.js installation:

```bash
> npx frontity serve
```

The site can then be visited from the browser using the address that the output from the command tells you it is listening on - this is likely to be http://localhost:3000.

The `build` directory can be deployed to any hosting that provides Node.js and can serve a Node.js app in order to make thse site publicly available.

In the next section we will look at deploying our site to one particular hosting service, namely Vercel.
