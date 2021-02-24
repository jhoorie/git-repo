STATUS: This seems to be functionally complete--alpha quality.

Repo is a repository management tool that Google built on top of Git. This fork provides a new `repo push` command. 

As part of the [Android development environment](https://source.android.com/source/developing), Repo unifies the many Git
repositories when necessary, does the uploads to the [revision control system](https://android-review.googlesource.com/),
and automates parts of the Android development workflow. Repo does not replace Git, it just makes it easier to work with
Git in the context of multiple repositories. The repo command is an executable Python script that you can put anywhere
in your path. In working with the Android source files, you will use Repo for across-network operations. For example,
with a single repo command you can pull files from multiple repositories into your local working copy.

This fork was enhanced to add:
1. A `repo push` command that performs an ordinary push of the topic branch on all repositories.  This allows you to
   push the topic branches to GitHub or GitLab, where you can create a pull request or merge request and get your code
   reviewed.  The existing `repo upload` command continues to upload to Gerrit as usual.
2. All operations are executed in the same order as defined in the manifest file.  In particular, `repo push` and
   `repo upload` push to the repositories in the same order that the ``<project>`` elements appear in the manifest file.

# Installing and using repo

## Prerequisites
repo requires Python 2.7 or above.  For Python 2.6 (untested), you must install the `ordereddict` package before using
repo.

## Installation
To install repo, follow the [repo installation instructions](https://source.android.com/source/downloading).  Of course
substiture this GitHub repository for the Google repository as required.

## Usage
The [Android Developing page](https://source.android.com/source/developing) shows you how to use repo.  If you want do
an ordinary push, use `repo push` command in place of `repo upload`.  If you wish to upload to Gerrit, use `repo upload`
as instructed.

The [manifest file reference](docs/manifest-format.txt) explains the contents of the manifest file that you use to
describe your repositories.

There is also a handy [repo Command Reference](https://source.android.com/source/using-repo).  This does not include
`repo push` documentation, but this command will print it:

    repo help push

# Developer information

The rest of this page is interesting only to developers, not users.

# Repository history

repo has a long history that makes it difficult to discover the canonical repository.

This repository is a fork of Google's https://gerrit.googlesource.com/git-repo/.  It appears that the same code is also served as https://android.googlesource.com/tools/repo/.  These two repository names have given rise to duplicate project names "git-repo" and "tools_repo" ("tools/repo" with '/' replaced with '_').

Due to the [shutdown of Google Code](http://google-opensource.blogspot.com/2015/03/farewell-to-google-code.html0), the original Google Code repo project https://code.google.com/p/git-repo/ has been archived for quite a while now, and is out of date.

## Resyncing with official google repo

This procedure comes to us from the [esrlabs/git-repo](https://github.com/esrlabs/git-repo) project.

For resyncing with the official google repo git, here are the commands for resyncing with the tag v1.12.33 of the official google repo:

    # add google git-repo remote with tag
    git remote add googlesource https://gerrit.googlesource.com/git-repo/
    git checkout v1.12.33 -b google-latest

    # checkout basis for resync
    git checkout google-git-repo-base -b update
    git merge --allow-unrelated-histories -Xtheirs --squash google-latest
    git commit -m "Update: google git-repo v1.12.33"
    git rebase stable

    # solve conflicts; keep portability in mind

    git checkout stable
    git rebase update

    # cleanup
    git branch -D update
    git branch -D google-latest


## Creating a new signed version

Prepare by creating your own GPG keys as described in the
[Pro Git](https://git-scm.com/book) Book
[Signing Your Work](https://git-scm.com/book/id/v2/Git-Tools-Signing-Your-Work) chapter.

Export an ASCII key:

    gpg --armor --export you@example.com > public.txt

Paste this key into file ``repo`` after the other keys.

Again in file ``repo``, Increment the second element of `KEYRING_VERSION`:

    KEYRING_VERSION = (1, 4)

In your Git working copy of `git-repo`, add and commit whatever files you have changed.

Sign the commit:
 
    git tag -s -u KEYID v0.4.16 -m "COMMENT"
    git push origin stable:stable
    git push origin v0.4.16

* For `KEYID`, use the ID of your key.  List your keys using the `gpg --list-keys` command.
* Replace `v0.4.16` With the actual version (note that there are two occurrences of this)
* Replace `COMMENT` with something more illuminating


## USER INPUT

First time IVAR-tool is opened. The workspace that will be used shall be empty.

### BASIC INPUT TEST

| Test ID  | Requirement | Implemented  | Result  | Comment  |
|:---|:---|:---|:---|
| ivar_52.2_u1  |  REQ_IVAR_52.2_w2050. |<span style="color:red">*YES/NO*</span> |*OK/NOK*  |    |
|ivar_51_u1  | REQ_IVAR_51_W2050. | *YES/NO*   |  *OK/NOK* |   |
|ivar_53_u1 | REQ_IVAR_53_w2050. | *YES/NO*   | *OK/NOK*  |   |
|ivar_54_u2 | REQ_IVAR_54_w2050. | *YES/NO*  |  *OK/NOK* |   |
|ivar_52.1_u1 |  REQ_IVAR_52.1_w2050. | *YES/NO* |  *OK/NOK* |   |
|ivar_51_u2 <br/>ivar_52.1_u2<br/>ivar_53_u2  |   REQ_IVAR_51_w2050<br/>REQ_IVAR_52.1_w2050<br/>REQ_IVAR_53_w2050. | *YES/NO*   |  *OK/NOK* |   |
| ivar_3_u1 | REQ_IVAR_3_w2040. | *YES/NO*  |  *OK/NOK*   |  |
| ivar_1_u1 | REQ_IVAR_1_w2040. |  *YES/NO* |  *OK/NOK*  |   |
| ivar_50_u1 | REQ_IVAR_50_w2050.|  *YES/NO*  |   *OK/NOK* |   |
| ivar_50_u2 | REQ_IVAR_50_w2050.   |*YES/NO*  |  *OK/NOK*  |   |
| ivar_6_u1 | REQ_IVAR_6_w2040.  | *YES/NO* |  *OK/NOK*  |   |
| ivar_2_u1<br/>ivar_7_u1<br/>ivar_20_u1 |   |   |   |
| ivar_10_u1  | REQ_IVAR_2_w2040<br/>REQ_IVAR_7_w2040<br/>REQ_IVAR_20_w2040.  | *YES/NO* |  *OK/NOK*  |   |
| ivar_61_u1 | REQ_IVAR_61_w2105.  | *YES/NO* |   *OK/NOK* |   |
| ivar_5_u1 |  REQ_IVAR_5_w2040.   | *YES/NO* |    *OK/NOK*|   |
| ivar_10_u2 |  REQ_IVAR_10_w2040. |  *YES/NO* |  *OK/NOK*  |   |
| ivar_10_u3 |  REQ_IVAR_10_w2040.  |  *YES/NO* |  *OK/NOK*  |   |
| ivar_9_u1 |  REQ_IVAR_9_w2040<br/>REQ_IVAR_20_w2040<br/>REQ_IVAR_50_w2050.  | *YES/NO* |   *OK/NOK* |   |
| ivar_1_u2 |   REQ_IVAR_1_w2040.  | *YES/NO* |   *OK/NOK* |   |
| ivar_49_g1 | REQ_IVAR_49_w2050.   | *YES/NO* |   *OK/NOK* |   |   |

### TEST OF GITLAB PATH

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_56_u1 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_56_u2 | *YES/NO* |  *OK/NOK*  |   |   |

## GRAPH GENERATION

### TEST MODULE VERSION

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
|  ivar_18_g1  | *YES/NO* |  *OK/NOK*  |   |
|  ivar_12_g1 | *YES/NO* |  *OK/NOK*    |

### TEST MODULE DESCRIPTION

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_18_g2 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_18_g3<br/>ivar_50_u5<br/>ivar_7_u3|  *YES/NO* |  *OK/NOK*  |   |

### TEST AUTHOR INFORMATION

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_18_g6 |  *YES/NO* |  *OK/NOK*   |   |   |
| ivar_18_g7<br/>ivar_50_u7<br/>ivar_7_u6 |  *YES/NO* |  *OK/NOK*   |   |   |

### TEST MAX INFORMATION

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_18_g8 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_18_g9<br/>ivar_50_u8<br/>ivar_7_u7 |  *YES/NO* |  *OK/NOK*  |   |

### TEST LIST OF DEPENDENCIES

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_5_g1<br/>ivar_7_u4 | *YES/NO* |  *OK/NOK*  |   |   |

### TEST WARNING/ERROR IN GRAPH

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_14_g1<br/>ivar_55_g1  | *YES/NO* |  *OK/NOK*  |   |   |

### TEST FAIL TO GENERATE GRAPH

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_8_g1  | *YES/NO* |  *OK/NOK*  |   |   |

### TEST UPDATE OF DEPENDENCIES

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_49_g2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_49_g3  | *YES/NO* |  *OK/NOK*  |   |   |

## GIT OPERATIONS

### OPERATION ON SINGLE REPOSITORY

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_16_r1  | *YES/NO* |  *OK/NOK*  |   |   |

### MULTIPLE REPOSITORIES IN A SINGLE WORKSPACE

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_38.1_r1<br/>ivar_44_r1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.2_r1 <br/>ivar_44_r3  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.3_r1<br/>ivar_44_r4  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.3_r2<br/>ivar_44_r5  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.8_r1<br/>ivar_44_r6  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.4_r1<br/>ivar_44_r7  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.8_r2<br/>ivar_44_r8  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.5_r1<br/>ivar_44_r9  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_39.1_r2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.6_r1<br/>ivar_39.2_r1<br/>ivar_44_r10  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.7_r1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.7_r2<br/>ivar_44_r12  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.7.1_r1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_38.11_r1<br/>ivar_44_r13   | *YES/NO* |  *OK/NOK*  |   |   |


### LOCAL REBASE

## WORKFLOW GUIDANCE

### DEFAULT CONFIGURATION

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_40.1.1_w1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_40.1.2_w1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_40.1.3_w1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_40.1.3_w2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_40.1.4_w1 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_40.1.5_w1<br/>ivar_40.1.6_w1<br/>ivar_40.2_w1  | *YES/NO* |  *OK/NOK*  |   |   |

## BUILD AND TEST OPERATIONS

### DEFAULT CONFIGURATION

### DEBUG BUILD

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_27.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_27.1_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_26.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_22_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_28_b1 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_23_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_25.1.1.2_b1<br/>ivar_46.1.1.1_b1<br/>ivar_48.1.2_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_25.1.1.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_46.1.2_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_48.1.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_45_b1 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_11_u1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_30.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_31.1.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_31.1.2_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_32.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_31.1.2_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_32.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_33.1_b1   | *YES/NO* |  *OK/NOK*  |   |   |


### BUILD RELEASE WITH ERRORS

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_27.1_b3  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_27.1_b4  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_26.1_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_25.1.1.2_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_25.1.1.1_b2  | *YES/NO* |  *OK/NOK*  |   |   |

### BUILD WITH SELECTABLE DEPENDENCIES

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_29.1_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_29.1_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_29.1_b3<br/>ivar_33.1_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_29.1_b5<br/>ivar_33.1_b3  | *YES/NO* |  *OK/NOK*  |   |   |

### BUILD AND ORBIS/SIMIAN

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_42_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_27.1_b5  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_43_b1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_42_b2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_42_b3<br/>ivar_43_b2<br/>ivar_35.1_t1<br/>ivar_37.1_t1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_35.1_t2<br/>ivar_37.1_t2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_35.1_t3<br/>ivar_37.1_t3  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_37.2_t1  | *YES/NO* |  *OK/NOK*  |   |   |

### UNIT TEST

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_34.1_t1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_34.1_t2<br/>ivar_37.1_t4  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_37.2_t  | *YES/NO* |  *OK/NOK*  |   |   |

### OSIM TEST

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_41.1_t1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_36.2_t1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_36.1_t1  | *YES/NO* |  *OK/NOK*  |   |   |

## FILE SYSTEM TESTS

### CLION AND FILE BROWSER TEST

|:---|:---|:---|:---|
| Test ID  | Implemented  | Result  | Comment  |
| ivar_47_f1 | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_47.1_f1  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_47_f2  | *YES/NO* |  *OK/NOK*  |   |   |
| ivar_47.2_f1  | *YES/NO* |  *OK/NOK*  |   |   |








