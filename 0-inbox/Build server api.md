clean package -Dsun.net.http.allowRestrictedHeaders=true -DexcludedGroups="buggy,integration"

add to run configuration 

Dsun.net.http.allowRestrictedHeaders=true - allows for Origin or Referer 
DexcludedGroups="buggy,integration" - skips tests 