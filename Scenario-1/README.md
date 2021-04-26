## Scenario_1 documentatiom
##### Found issue
* `` Transform `` section was missing in template, for SAM template this section is mandatory

* ``parameters`` section's values was missing

* No properties  with ``Name`` in ``AWS:IAM:Role`` resource exist , it should be ``RoleName``

* In ``rLambdaFunction``  resource, ``runtime`` properties was missing

* In ``rLambdaFunction``  resource, value of ``Handler`` properties was ``lambda.lambda_handler``, but lambda function name is ``handler``.Value of handler properties should be ``<filename>.<lambda_functionname>`` so that correct value would be ``lambda.handler``

* In ``rLambdaFunctionAliasErrorAlarm`` resource , value of dimensions properties is alias name of ``rLambdaFunction`` resource is used, but not any properties included in ``rLambdaFunction`` resource to have a alias. So to create Alias ``AutoPublishAlias`` properties included in ``rLambdaFunction`` resource

* Value of ``Role`` properties  in ``rLambdaFunction`` resource should be arn of role. We can't find ``Arn`` value by only reference of logical id of AWS:IAM:Role resources. So to get arn, need to use intrinsic function ``!GetAtt <logicalId>.arn``. In this template to attcach role with ``rLambdaFunction`` resource, need to use  ``!GetAtt.rLambdaFunctionRole.arn``

##### Steps to deploy
* Fix the ``template_1.yaml`` with help of above details (already fixed)
* Create S3 bucket with name of ``pArtifactS3BucketName`` parameter value
* upload ``template_1.yaml and lambda zip code`` in S3 bucket
* Manualy create ``stack`` using cloudformation service