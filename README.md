# Containerizing the app

1. Forked the repository 
2. Setup a new AWS account for this project
3. I haven't worked with vuejs before (Its mostly been python and other backend services). I believe it was time I get the basics of vuejs before I could think of automating it. While the ideas and concepts of the deployment and packaging would remian the same, understanding how the framework operates will help make logical choices.
4. Built a new app locally using vue-cli. Ran into some issues where the cli was of the older version and its remnants were left over even after removing it. Cleaned everything up by hand and installed the latest vue cli (version 4+). It appers to work as expected now.
5. Deployed the weather app manually by hand (npm install, build and serve). The app seems to be working.
6. Trying to serve it using a nginx locally (still without docker). Referring to their offical docs that I found at https://cli.vuejs.org/guide/deployment.html
7. Now that I've got the app working and understanding of how vue operates, working on the Dockerfile to containerze the app
8. I've run into an error while containerizing the app. Upon inspection using the dev tools of chrome, it seems that the app is looking for files in http://serverip/progressive-weather-app directory, while we have simply deployed everything directly. Figures that I can modify the base values in the vue.config.js. Updated the value of "baseUrl" to "/". Rebuilt the image and now it appears to be working as expected.


# Setting up an EKS cluster
1. Using eksctl to create the cluster in us-east-2 region
2. install awscli, kubectl and eksctl
3. Kubernetes cluster is now up and running
4. Setup the app deployment and service manually to ensure that its actually working.

# Setting up CI CD Pipeline
I thought of using Jenkins as first as I've used it for first. However, I've been meaning to learn Github actions for a while but didn't get the chance / time. Using this opportunity to go through Github's docs and leverage their "actions".

1. Setup the CI workflow which basically builds the docker file
2. Setup docker hub secrets in the Github repo
3. Using those secrets as environment variables to push the image to my dockerhub account
4. Setup EKS kube-config as a secret along with other data
5. Pushed the changes to EKS

# Output
1. You can find the application at - http://ae5ad7007d18d43ad9a3354cfed03081-1357377340.us-east-2.elb.amazonaws.com/
2. I can give you access to the bastion box where all of this is setup, but its all in the git repo anyway.
3. You can find the screenshot of the CI CD pipeline here -> https://i.imgur.com/K7QSMQj.png
4. Github actions code for the ci/cd pipeline can be found in .github/workflow/main.yaml of the same repository 

# What could be improved?
1. I am currently using an opensource docker image with kubectl to deploy to EKS. I could build my own and optimize it further for faster build times
2. The application is currently deployed as a single docker image. I could potentially host the static assets on an external source such as AWS S3.
3. There is no auto-scaling in place here, I could potentially set one up but may be that's for another day.
4. Add an SSL cert ofcourse 
