# serverspec-infra-testing

Example of using Serverspec to test infrastructure

![Final Environment](https://user-images.githubusercontent.com/3911650/39964780-7994a4fa-5649-11e8-8695-e345ca893785.png)

## Getting Started

Deploy the CloudFormation `infrastructure/cloudformation.json` template. The template creates a user with the following credentials and minimal required permisisons to complete the Lab:

- Username: _student_
- Password: _password_

## Instructions

1. In the Cloud9 environment, install Serverspec:

    ```sh
    gem install serverspec
    ```

1. Initialize a spec directory for UN*X targets, SSH backend connections, no Vagrant instance, and named proxy:

    ```sh
    serverspec-init
    ```

1. Add a proxy SSH config to your ~/.ssh/config file

    ```config
    HOST proxy
        HostName 10.0.1.100
        User serverspec
    EOF
    ```

1. Run the default tests with `rake spec` and use the SSH password of `1Cloud_Academy_Labs!`

1. Repeat the process for the app instance (10.0.2.100)

1. Run Serverspec in a container with the following commands:

    ```sh
    docker run -v "$(pwd):/serverspec:ro" -v "/home/ec2-user/.ssh:/root/.ssh:ro" -t --rm lrakai/serverspec:1.0.0 spec
    ```

## Cleaning Up

Delete the CloudFormation stack to remove all the resources used in the Lab.