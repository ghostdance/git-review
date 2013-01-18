# git-review

Place git-review somewhere in your path, and use it like any other built-in git command:

    git review list
    git review list --all
    git review list --all --compact
    git review pull
    git review push
    git review mark 0 HEAD -m "please review"

## Adding Review Notes

Code review notes managed by git-review consist of remarks (text) and a flag. Each time
you annotate a commit, a flag value is required. Review flags mean roughly the below:

     0 = "please review this"
    >0 = "i feel good about this code"
    <0 = "i think this code might bear another look, maybe some changes"

To mark a commit as needing review, do the following from within the repo's work tree:

    git review mark 0 HEAD -m "can somebody please take a look at this?"

The above assumes the commit in question is at HEAD. If it's a commit with the SHA e09ecbb8cb4c11fba8998b025bdb031c4ae87fe8
you'd do this:

    git review mark 0 e09ecbb8cb4c11fba8998b025bdb031c4ae87fe8 -m "can somebody please take a look at this?"

If you wanted to mark both HEAD and e09ec... as needing review, you'd do this:

    git review mark 0 HEAD e09ecbb8cb4c11fba8998b025bdb031c4ae87fe8 -m "can somebody please take a look at this?"

To mark a commit as being in need of work:

    git review mark -1 HEAD -m "Can you remove the debugging statements? Other than that, should be ok."

And when it's a go:

    git review mark +25 HEAD -m "This looks great!"


## Listing Review Requests

You can use git-review's ```list``` command to list commits with review data. By default, the ```list``` command
will display commit logs and review notes for commits with *pending* (flag = 0) review requests.

    git review list

To list *all* commits with review information, use the ```--all``` switch:

    git review list --all

And for a compact listing, including just the commit hash and latest review flag, use the ```--compact``` switch:

    git review list --all --compact

## Collaborating Using Notes

The ```push``` and ```pull``` commands allow git-review to consume and publish notes from and to remote repositories (like Github).

To pull review data from the default remote, ```origin```, simply do the following:

    git review pull

To pull review data from a remote called ```work```:

    git review pull work

To push review data to a remote repository (```origin```):

    git review push

Or to be more specific (```work```):

    git review push work

It is **strongly** advised that you do a ```git review pull``` before doing a ```git review push```.
