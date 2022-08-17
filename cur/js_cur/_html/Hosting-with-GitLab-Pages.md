# Hosting your static websites with GitLab Pages

With GitLab Pages we can effortlessly publish our static pages/websites and have it online with either url generated from your-account-name.gitlab.io/name-of-your-repo-project or with a custom domain. Basically it is doing same as GitHub pages but also allows us to run some static generator's made websites.

1. Initialize new git project in the root folder of your website if you have not done it yet.

2. Create a repo on GitLab and add a remote origin to your local project.

3. Make sure that your homepage is called index.html, it's the default entry point for any static website.

4. Create a folder `public` in the root of your project and move all the files there (html,css,js,images, etc.)

5. In the root of your project create a file called `.gitlab-ci.yml` with the following content:

```
image: alpine:latest
pages:
  stage: deploy
  script:
  - echo 'Nothing to do...'
  artifacts:
    paths:
    - public/
```

6. Push all the code to your GitLab repo.

7. On GitLab's project page in the CI/CD section check Pipelines and Jobs -- they should be green and completed.

8. In Settings -> Pages section you will have a url of your hosted website. After about 10-20 minutes your website would be live there.
