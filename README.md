# Publish from local machine

* Create access token in github
![001-CreateAccessToken.png](./images/001-CreateAccessToken.png)
* Create ```.npmrc``` in the same folder where ```packge.json``` is located.
  Because this ```.npmrc``` contains secret it should not be pushed to the remote repo so it has to be added to `.gitignore`.

  ```
  @kicaj29:registry=https://npm.pkg.github.com/
  //npm.pkg.github.com/:_authToken=[TOKEN_VALUE]
  ```
  If the token would be commit to the repo then github will remove it very soon, more [here](https://stackoverflow.com/questions/53579650/github-api-personal-access-token-removes-itself).

* In `package.json` of the library add entry: ```"repository": "https://github.com/kicaj29/github-action-publish-npm"```.
  Thx to this package name does not have to match to repository name, more [here](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry#publishing-multiple-packages-to-the-same-repository).

* Next run

  ```
  cd my-workspace/
  ng build @kicaj29/lib1 --prod
  cd dist/kicaj29/lib1
  npm publish
  ```

  >NOTE: I had very weird issue with of failing authentication. If it would happen again try the following 2 options before running `npm publish`.

  Option 1: run npm login.   
  ```
  npm login --scope=@OWNER --registry=https://npm.pkg.github.com
  Username: kicaj29
  Password: TOKEN (it is not password to user account!)
  Email: PUBLIC-EMAIL-ADDRESS
  ```

  Option 2: copy `.npmrc` to `dist/kicaj29/lib1`.
# links
https://angular.io/guide/creating-libraries   
https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry   
https://medium.com/@windix/host-and-publish-npm-package-on-github-bb419a2acfd3   

