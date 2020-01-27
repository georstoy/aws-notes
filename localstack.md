# deploy cloudformation template
`npm run build && touch ./tmp/myStack.template.yml && cdk synth --no-stage myStack > ./tmp/myStack.template.yml` \
`aws --endpoint-url=http://localhost:4581 cloudformation deploy --template-file ./tmp/myStack.template.yml --stack-name myStack`

# list deployed stacks
    should be able to see the stack \
`aws --endpoint-url=http://localhost:4581 cloudformation list-stacks`