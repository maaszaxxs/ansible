
> **Note**: When you attempt any CircleCI exercise, you should comment out the Jobs and Workflows from other exercises. This will ensure that you do not end up creating unnecessary EC2, S3, CloudFront resources in your AWS console.

### 1. Exercise: Infrastructure Creation
Files relevant for this exercise are:
```bash
└── template.yml            # Change the KeyName property value, as applicable to you
└── .circleci
    └── config.yml          # Look for the create_infrastructure Job
```


### 2. Exercise: Config and Deployment
**Prerequisite**:
- Create an EC2 instance and note it's public IP address
- Add the contents of your PEM file to the SSH keys in your Circle CI account to get the fingerprints

Files relevant for this exercise are:
```bash        
├── ansible.cfg             
└── .circleci
    └── config.yml          # Look for the configure_infrastructure Job
```


### 3. Exercise: Smoke Testing
Files relevant for this exercise are:
```bash           
└── .circleci
    └── config.yml          # Look for the smoke_test Job
```


### 4. Exercise - Rollback
Files relevant for this exercise are:
```bash    
└── template.yml            # Change the KeyName property value, as applicable to you       
└── .circleci
    └── config.yml          # Look for the create_infrastructure Job and destroy_environment command.
```


### 5. Exercise: Promote to Production
**Prerequisite**:
- An S3 bucket (say `mybucket644752792305`) containing a sample `index.html` file created manually in your AWS console.
- Enable the Static website hosting in that bucket.
- Use the command below to create a  CloudFront Distribution
```bash
 aws cloudformation deploy \
 --template-file cloudfront.yml \
 --stack-name production-distro \
 --parameter-overrides PipelineID="mybucket644752792305"
 ```
Files relevant for this exercise are:
```bash  
├── bucket.yml          # Creates a new bucket and bucket policy.       
├── cloudfront.yml      # Creates a Cloudfront Distribution that will connect to the existing ^ bucket.
├── error.html
├── index.html  
# Four Jobs: create_and_deploy_front_end, get_last_deployment_id, promote_to_production, and clean_up_old_front_end
└── .circleci
    └── config.yml
