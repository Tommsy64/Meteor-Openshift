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
We don't need the template so lets reset the git history.

1. Checkout ```git checkout --orphan latest_branch```
2. Delete the branch ```git branch -D master```
3. Copy the contents of this repository into the branch
```
git remote add meteor-openshift -m master https://github.com/Tommsy64/Meteor-Openshift.git
git pull -s recursive -X theirs meteor-openshift master
```

Now you can build your meteor app
```
cd path/to/your/meteorapp
meteor build path/to/your/openshiftmeteorapp --directory --server-only
```

4. Add all the files ```git add -A```
5. Commit the changes ```git commit -am "First commit"```
6. Rename the current branch to master ```git branch -m master```
7. Finally, force update your repository ```git push -f origin master```