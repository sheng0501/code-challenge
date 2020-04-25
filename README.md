This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

### running locally using docker

If you want to run the server locally you need to follow the following step:

```

docker build -t my-app .
# make sure port 3000 is not being used
docker run --expose=3000 my-app

```

## CI/CD

This repo follows the circleci's [demo setup](https://github.com/CircleCI-Public/circleci-demo-aws-ecs-ecr) closely.
Though the pipeline is setup, it is a very rudimentary configuration, and will definitely need some tweaking for production use.
Also, it is crucial to include testing as well, which the project currently does not have any. Without automated testing with high coverage, it is not advised to use the pipeline. 

### Resource creation

There is a first one time setup by terraform (please have at least v0.12 installed). Which can be done through the following command:

```
cd .terraform
terraform init
# Review the plan
terraform plan
# Apply the plan to create the AWS resources
terraform apply
```

Make sure you have updated .terraform/terraform.tfvars with the needed infor before running the above command. Specifically you need to provide aws credential which has
sufficient permission to create the resources. 

### deployment

deployment is very straightforward after the one time setup by terraform. It goes through circleci. Simply merge your feature branch to master will trigger a 
circleci build which uses the ecs and ecr orbs. The build is in two step: first, it builds and push a new docker image with latest tag to the ecr. Second it uses the new image and tag
to update the ecs service definition, and trigger a deployment.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
