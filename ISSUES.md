bugs i found

p1: migration has 3 separate buttons with no rollback. if azure upload fails after db save, the problem is stuck in db with missing testcases.

p2: clicking migrate again just overwrites the db row silently without checking polygon revision or asking confirmation.

p3: invalid problem id or polygon timeout throws a raw 500 crash page instead of showing a user friendly error.

c1: polygon api calls and azure uploads run synchronously in the view. for big test suites this blocks the worker and hits 504 timeouts.

c2: azure sdk is imported directly in views.py without any storage interface, making it hard to test locally or swap to s3.

c3: line 540 truncates test inputs and outputs to 260 chars. empty tests are also dropped, so db has broken test data.

edge cases:

q1: 0 sample tests means SampleTestCase table is empty, so the problem description page shows no examples at all.

q2: reducing from 20 to 12 tests leaves 8 ghost tests in db because it only updates rows 0-11 and never deletes the rest.

q3: two problems named two sum get the same slug. second one crashes with unique constraint error on slug.

q4: data lost is text past 260 chars, stripped trailing whitespace, and empty tests. breaks judging if evaluated against db.
