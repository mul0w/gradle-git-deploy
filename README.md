# gradle-git-deploy
Deployment of gradle based libs on Git repositories

This is a tooltip to publish directly your libraries to a Git repository like Github or Bitbucket.
You can find more on [this post](https://medium.com/@Mul0w/publish-with-gradle-on-bitbucket-1463236dc460).

## Usage

### 1. Global gradle.properties
Setup your global gradle settings in your home gradle.properties file (usually located in ~/.gradle/).

```properties
REPOSITORY_USERNAME=username
REPOSITORY_PASSWORD=passwd
```

### 2. Project & module level gradle.properties
You can setup (maybe it's already done) your properties at a project and module level. You may for example provide a sample module which you don't want to deploy because it makes no sense, but some of your properties are "project level". An example could be like this : 

Project : 
```properties
VERSION_NAME=X.Y.Z[-SNAPSHOT]
VERSION_CODE=XYZ
GROUP=group_id

POM_DESCRIPTION=Bla bla bla
POM_URL=Lib Url
POM_SCM_URL=Scm Url
POM_SCM_CONNECTION=...
POM_SCM_DEV_CONNECTION=...
POM_LICENCE_NAME=...
POM_LICENCE_URL=...
POM_LICENCE_DIST=repo
POM_DEVELOPER_ID=you
POM_DEVELOPER_NAME=You
POM_DEVELOPER_EMAIL=You@...
```

& library module :
```properties
POM_NAME=Your Great Lib
POM_ARTIFACT_ID=lib_artifact_id
POM_PACKAGING=aar(or jar)
```

### 3. Deploy module

Then, you're just 2 steps closer to deploy your module, the first one is to update your gradle build file to add the dependency on the deploy file:

```groovy
apply from: 'https://raw.githubusercontent.com/mul0w/gradle-git-deploy/master/deploy.gradle'
```

And now, build (& clean, if necessary), & upload to your repo:

```bash
$ gradle [clean build] uploadArchives
```
	
## License

    Copyright 2015 Stephane Virte

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.