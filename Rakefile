task :default => :deploy

desc "Deploy to S3"
task :deploy do
  deploy_to
  sh "jekyll"
  sh "s3cmd sync --exclude 'assets/*' _site/* #{@s3_bucket_url}"
  sh "s3cmd sync --add-header 'Expires: Thu, 6 Feb 2020 00:00:00 GMT' _site/assets/* #{@s3_bucket_url}/assets/"
  sh "s3cmd setacl --recursive --acl-public #{@s3_bucket_url}/"
end

desc "Delete any deleted files, and do a deploy"
task :detailed_deploy do
  deploy_to
  sh "jekyll"
  sh "s3cmd sync --delete-removed --exclude 'assets/*' _site/* #{@s3_bucket_url}" # this will now delete the whole assets folder
  sh "s3cmd sync --add-header 'Expires: Thu, 6 Feb 2020 00:00:00 GMT' _site/assets/* #{@s3_bucket_url}/assets/" # dont delete-removed again, as this would then delete the html files!
  sh "s3cmd setacl --recursive --acl-public #{@s3_bucket_url}/"
end

def deploy_to
  @s3_bucket_url = "s3://todo_ourbucketname"
end

# with bucket www.profitably.com.s3.amazonaws.com site runs at http://www.profitably.com.s3.amazonaws.com.s3.amazonaws.com/index.html
