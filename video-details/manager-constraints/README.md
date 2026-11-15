This folder contains files used to recreate the scenario mentioned in the video. On Turn 13, serving C3’s pasta 
versus taking C4’s order can lead to victory or defeat.

The files are to be run on Stage 1 of the repository, which can be found using the Stage-1 tag in the repository.

```bash
   git checkout stage-1
   javac -d out $(find src -name '*.java')
   git show main:video-details/manager-constraints/stage1_t13_order_c4_input.txt | NO_COLOR=1 java -cp out cli.Main
```
