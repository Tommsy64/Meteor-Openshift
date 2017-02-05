# Openshift-Meteor

## Setting up Openshift Meteor

Install the Openshift [Client Tools](https://developers.openshift.com/managing-your-applications/client-tools.html).

Create an Openshift app with Node and MongoDB 3.x

```
rhc app create openshiftmeteorapp \
  nodejs-0.10 \
  https://raw.githubusercontent.com/icflorescu/openshift-cartridge-mongodb/master/metadata/manifest.yml
```

`rhc` will automatically clone the app repository with a template in it.
```
cd openshiftmeteorapp
```
The template is not needed, so reset the git history.

1. Checkout ```git checkout --orphan latest_branch```
2. Delete the master branch ```git branch -D master```
3. Delete the contents of the new branch and unstage changes.
  ```
  rm -r * .openshift/
  git add -A
  ```
4. Copy the contents of this repository into the new branch.
  
  ```
  git remote add meteor-openshift -m master https://github.com/Tommsy64/Meteor-Openshift.git
  git pull -s recursive -X theirs meteor-openshift master
  git remote remove meteor-openshift
  ```

5. Now you can build your Meteor app:
  
  ```
  (METEOR_APP_PATH=path/to/your/meteorapp && OPENSHIFT_APP_PATH=path/to/your/openshiftmeteorapp && cd $METEOR_APP_PATH && meteor build $OPENSHIFT_APP_PATH --directory --server-only)
  ```
6. Add all the changes ```git add -A```
7. Commit the changes ```git commit -am "First deployment"```
8. Rename the current branch to master ```git branch -m master```
9. Finally, force update your repository ```git push -f --set-upstream origin master```. This will take a couple of minutes.