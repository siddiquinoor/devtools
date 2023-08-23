# MongoDB Atlas using AWS CloudFormation Template

1. Using AWS Partner Solutions (previously AWS Quick Starts)

    https://aws.amazon.com/quickstart/?solutions-all.sort-by=item.additionalFields.sortDate&solutions-all.sort-order=desc&awsf.filter-content-type=*all&awsf.filter-tech-category=*all&awsf.filter-industry=*all&solutions-all.q=mongodb&solutions-all.q_operator=AND

1. Select the 3rd option MongoDB Atlas

    https://aws.amazon.com/solutions/partners/mongodb-atlas/

1. Click on How to deploy and then "Deploy MongoDB Atlas without VPC peering"

1. Change the Zone to Europe (London)

1. Use previously created Profile Name for MongoDB Atlas API secret
    
    Ref: https://github.com/mongodb/mongodbatlas-cloudformation-resources/blob/master/examples/README.md
    Ref: https://github.com/mongodb/mongodbatlas-cloudformation-resources/blob/master/examples/profile-secret.yaml

1. Find Organization ID from MongoDB Atlas and paste on OrgId

1. Enter a Project Name i.e. "GCC"

1. Enter a Name of new cluster i.e. "gcc-api"

1. Change AWS Region for Atlas cluster

1. Enter a new MongoDB Atlas Database User Name

1. Enter a new MongoDB Atlas Database User Password

1. Change the Quick Start S3 bucket Region

1. Next and Next and complete


