You can get started by using these images in your Dockerfile and coping your function code into the /var/task folder in your image.

Example Dockerfile below:

FROM public.ecr.aws/lambda/python:3.12

# Copy function code
COPY app.py ${LAMBDA_TASK_ROOT}

# Set the CMD to your handler (could also be done as a parameter override outside of the Dockerfile)
CMD [ "app.handler" ]
You can then locally test your function using the docker build and docker run commands.

To build you image:

docker build -t <image name> .
To run your image locally:

docker run -p 9000:8080 <image name>
In a separate terminal, you can then locally invoke the function using cURL:

curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{"payload":"hello world!"}'
To learn more on deploying the function to ECR, check out the AWS documentation on Creating a repository and Pushing an image