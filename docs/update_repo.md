# How to Update Repository

This repository is a branded version of the [foreman-operations-collection](https://github.com/theforeman/foreman-operations-collection) and requires some consideration when updating.
The basic update is to merge in upstream changes from a target release version and then apply branding. However, new roles may need additional testing added to them.

```
git checkout -b update-to-<target tag>
git remote add upstream https://github.com/theforeman/foreman-operations-collection
git fetch upstream
git merge upstream/<target tag>
make branding
```

Now inspect the changes that are made and manually fix any irregularities.

## New Roles

When new roles are added from upstream there are two options for dealing with them:

 1. A new role that isn't being shipped with Satellite. This role should be added to the Makefile removal list and then re-run `make branding`.
 2. A new role that is being shipped with Satellite. This role should have a test folder `roles/<new role>/molecule/satellite` added to it.
    This test folder should include any testing needed to verify this role in a Satellite context.
