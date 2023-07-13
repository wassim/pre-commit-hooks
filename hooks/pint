#!/bin/bash

# Pint needs to run in the actual working directory, so we need to find that
REAL_DIR=$(git rev-parse --show-toplevel)

# Get a list of all staged PHP files
FILES=$(git diff --cached --name-only --diff-filter=d -- '*.php')

if [ "$FILES" = "" ]; then
    exit 0
fi

# Flag to check if anything fails
FAILED=0

# Run Pint on each staged PHP file
for FILE in $FILES
do
    cd "$REAL_DIR" || exit
    ./vendor/bin/pint "$FILE"
    if [ "$?" != 0 ]; then
        echo "Pint failed on $FILE"
        FAILED=1
    fi
done

# If any file failed, then fail the commit
if [ "$FAILED" = 1 ]; then
    exit 1
fi

exit 0
