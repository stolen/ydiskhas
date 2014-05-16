YDiskHas
========

A little utility that can tell if a given file has been already uploaded by
someone to Yandex.Disk by using using its API's deduplication check.

Installation (Go 1.2): `$ go get github.com/dchest/ydiskhas`

Potential uses are described, for example, here:
["Side channels in cloud services, the case of deduplication in cloud storage"](http://www.pinkas.net/PAPERS/hps.pdf).

One example:

Step 1. Send a form to Alice and ask her to fill it and save to Yandex.Disk.

*form.txt*:

    Alice, do you love Bob?  

    [ ] Yes  [ ] No


Step 2. Generate two files:

*form-yes.txt*:

    Alice, do you love Bob?  

    [x] Yes  [ ] No


*form-no.txt*:

    Alice, you love Bob?  

    [ ] Yes  [x] No

Step 3. Run `yadiskhas` on both files:

    $ yadiskhas -login=YourYDiskLogin -password=YourPassword form-yes.txt

    (╯°□°)╯︵ ┻━┻
    File does not exist on Yandex.Disk.


    $ yadiskhas -login=YourYDiskLogin -password=YourPassword form-no.txt

    ˙ ͜ʟ˙
    FILE EXISTS on Yandex.Disk!


...and discover that Alice doesn't love Bob :-(