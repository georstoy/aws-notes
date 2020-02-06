# Cloudformation
`aws cloudformation list-exports`

# Cloud Environment
 - account id = `$(aws sts get-caller-identity --query "Account" --output text)`
 - region = `$(aws configure get region)`