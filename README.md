# Release Process

This repo is intented to be used to facilitate the release process. All CORD modules that are intended 
to be released with any given cord release should be integrated into this repository. 

## Source the environment to get git commands

    source bash_profile


## Get all latest commited code and update submodules

    git cpull -r

## Create Release Branch in local repo as well as in submodules

    git ccheckout -r -b $RELEASE_VERSION

## Update .gitreview locally and submodules

    update-gitreview all $RELEASE_VERSION
    git submodule foreach --recursive 'update-gitreview $name $RELEASE_VERSION'

## Update CORD ONOS application versions

    cd cord/components/cord-onos-publisher
    update-versions $RELEASE_VERSION $ONOS_VERSION
    cd -

## Commit all changes (which also updates submodule references)

    git ccommit -r -a -m "Preparing Release $RELEASE_VERSION"
    git ctag $RELEASE_VERSION

## Submit changes for review

    git creview

## Checkout master

    git ccheckout master

## Update CORD ONOS Applications to SNAPSHOTS

    cd cord/components/cord-onos-publisher
    update-versions $SNAPSHOT_VERSION $ONOS_VERSION
    cd -

## Push everything up for Review

    git ccommit -r -a -m "Updating ONOS applications to $SNAPSHOT version"
    git creview
