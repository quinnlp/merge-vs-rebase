# Merge vs Rebase

This repo shows the differences between merge and rebase.

*I was confusing myself in the lab. Hope this is easier to follow.*

## In this repo, I did the following:

1. created `file.txt` in `060028e` on `main`
1. branched off from `main` to `diffbranch`
   1. added a line to `file.txt` in `c0e37e5` on `diffbranch`
   1. added a line to `file.txt` in `53fd3de` on `diffbranch`
1. added a line to `file.txt` in `37cf820` on `main`
1. branched off from `diffbranch` to `mergebranch`
   1. merged `main` into `mergebranch` (`git merge main`)
      - this created the merge commit `9f29798` to merge the histories of `main` and `mergebranch`
1. branched off from `diffbranch` to `rebasebranch`
   1. rebased `rebasebranch` against `main` (`git rebase main`)
      - this changed the base of `rebasebranch` from `060028e` to `37cf820` and reapplied `c0e37e5` and `53fd3de` as `b6b4416` and `3f00482` respectively, changing the history of `rebasebranch`

You can see how the git histories look here:

```sh
quinnpham@Quinns-MacBook-Pro merge-vs-rebase % git log --oneline --graph main
* 37cf820 (HEAD -> main, origin/main) commit main line 1
* 060028e Added first file
quinnpham@Quinns-MacBook-Pro merge-vs-rebase % git log --oneline --graph diffbranch
* 53fd3de (origin/diffbranch, diffbranch) branch commit line 2
* c0e37e5 branch commit line 1
* 060028e Added first file
quinnpham@Quinns-MacBook-Pro merge-vs-rebase % git log --oneline --graph mergebranch
*   9f29798 (origin/mergebranch, mergebranch) Merge branch 'main' into mergebranch
|\
| * 37cf820 (HEAD -> main, origin/main) commit main line 1
* | 53fd3de (origin/diffbranch, diffbranch) branch commit line 2
* | c0e37e5 branch commit line 1
|/
* 060028e Added first file
quinnpham@Quinns-MacBook-Pro merge-vs-rebase % git log --oneline --graph rebasebranch
* 3f00482 (origin/rebasebranch, rebasebranch) branch commit line 2
* b6b4416 branch commit line 1
* 37cf820 (HEAD -> main, origin/main) commit main line 1
* 060028e Added first file
quinnpham@Quinns-MacBook-Pro merge-vs-rebase %
```

*I'm not really sure what had me so confused in the lab. I think I was rebasing in the wrong direction (rebasing `main` against the `featurebranch` instead of the other way around).*

# Lessons

- merging creates a new "merge" commit to merge the histories of 2 branches together
- rebasing changes the history of the branch you are rebasing by moving the base of the branch to the head of the branch you are rebasing against and reapplying the commits on the branch you are rebasing  
- merging is always "safe"
- you should never rebase commits that you have pushed to remote because you will change the history of the remote repository
- this stuff can be confusing :P
