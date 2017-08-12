# pixilate
A secure serverless image hosting solution for posting visual media to sites with restrictive community guidelines

## Technology
- Mithril.js SPA
- AWS Cognito with Facebook Login for authentication and authorization
- AWS S3 for secure media storage, one S3 bucket per group for ease of control
- AWS CloudFormation for configuring AWS resources and permissions
- AWS Lambdas for any needed server processes.  None are anticipated for the immidiate stages of the project


## Basic Overview

#### Index page
- user visits visit main page
- if user is not logged in, the user is redirected to FB for login and authentication; otherwise
- user's FB groups are listed
- user selects a FB group they are a member of
- user is directed to [site]/fb/group/[group_id]

#### Group page
- the user's membership in the selected group is verified
- the user see an image upload form, as well as a grid of other images recently posted for the selected facebook group by any members
- the user can select an image to upload from his device
- if the user is a group admin on facebook, they additionally see an option for each photo to remove the photo.

#### Image upload process
- the user uploads an image from his local machine via a webform
- the image is directly uploaded to S3 in two versions
  - the original version
  - a pixilated version
- the user is requested to confirm they would like to post the uploaded image to the group
- the pixilated version of the image is posted to the group, along with a link to the full, unpixilated image.

## Considerations
#### Preventing Facebook from viewing the full image
- Only members of the group will have access to see any photos
- Facebook's own IP ranges can be blocked entirely, or can be served pixilated images always

#### Costs
- while the S3 storage costs money, it is neglible ($0.03/GB/month)
- by using per group S3 buckets, usage can be easily tracked for cost accounting purposes
- the service could easily be ad supported
- media could be deleted after X number of days, minimizing costs at the expense of group history

## Future Additions
- Support more than just FB groups.
- Support more media types - video
- Support client side media encryption, so even the server doesn't have access to the content

