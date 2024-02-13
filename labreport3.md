Lab Report 2

Benjamin Scheerger

Cse-15L

# Buggy Code

## Failure Inducing Input 

 ` @Test 
	public void testReverseinplace3() {
    int[] input1 = {1, 2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3, 2, 1 }, input1);
	}`

## Passing Input 

 `@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}`

## Failure Symptom
 
![Image](FailureSymptom.PNG)

 ## Bugged Code
 
  `static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }`

 ## Fixed Code
 
 `  static void reverseInPlace(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[i];
    }
    for (int i = 0; i < arr.length; i+=1) {
      arr[i] = newArray[arr.length - i -1];
    }
  }`

The fix for this code addresses the issue of actively changing the array as it is reversed. In the original code, `arr[i] = arr[arr.length - i - 1]` is changing `arr` as it reverses it, so the addition of `newArray` as a deep copy of the original array, makes it so `arr` can be accurately reversed. 

# Find Command
## find -type
### Example 1
`$ find . -type d
.
./911report
./biomed
./government
./government/About_LSC
./government/Alcohol_Problems
./government/Env_Prot_Agen
./government/Gen_Account_Office
./government/Media
./government/Post_Rate_Comm
./plos`

This command searches for and prints the directories contained in the directory that you run it on, which is useful in case you want a specific directory name, you want to quickly see a list of the directories, or a multitude of other reasons.

### Example 2
`$ find . -type f
./chapter-1.txt
./chapter-10.txt
./chapter-11.txt
./chapter-12.txt
./chapter-13.1.txt
./chapter-13.2.txt
./chapter-13.3.txt
./chapter-13.4.txt
./chapter-13.5.txt
./chapter-2.txt
./chapter-3.txt
./chapter-5.txt
./chapter-6.txt
./chapter-7.txt
./chapter-8.txt
./chapter-9.txt
./preface.txt`

This command searches for and prints all the files in a directory. For this example, I ran the command on the `911reports` directory as running it on `/.technical` returned too many files to paste here. This is useful if you want to see all the files in a directory in a succinct list.

## find -size
### Example 1
`$ find . -size +100
./About_LSC/commission_report.txt
./About_LSC/State_Planning_Report.txt
./About_LSC/Strategic_report.txt
./Alcohol_Problems/Session3-PDF.txt
./Alcohol_Problems/Session4-PDF.txt
./Env_Prot_Agen/atx1-6.txt
./Env_Prot_Agen/bill.txt
./Env_Prot_Agen/ctf1-6.txt
./Env_Prot_Agen/ctf7-10.txt
./Env_Prot_Agen/ctm4-10.txt
./Env_Prot_Agen/jeffordslieberm.txt
./Env_Prot_Agen/multi102902.txt
./Env_Prot_Agen/section-by-section_summary.txt
./Env_Prot_Agen/tech_adden.txt
./Gen_Account_Office/ai00134.txt
./Gen_Account_Office/ai2132.txt
./Gen_Account_Office/ai9868.txt
./Gen_Account_Office/d01376g.txt
./Gen_Account_Office/d01591sp.txt
./Gen_Account_Office/d0269g.txt
./Gen_Account_Office/d02701.txt
./Gen_Account_Office/d03232sp.txt
./Gen_Account_Office/d03419sp.txt
./Gen_Account_Office/gg96118.txt
./Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
./Gen_Account_Office/im814.txt
./Gen_Account_Office/July11-2001_gg00172r.txt
./Gen_Account_Office/June30-2000_gg00135r.txt
./Gen_Account_Office/May1998_ai98068.txt
./Gen_Account_Office/Oct15-2001_d0224.txt
./Gen_Account_Office/pe1019.txt
./Gen_Account_Office/Sept14-2002_d011070.txt
./Gen_Account_Office/Sept27-2002_d02966.txt
./Gen_Account_Office/Statements_Feb28-1997_volume.txt
./Gen_Account_Office/Testimony_cg00010t.txt
./Gen_Account_Office/Testimony_Jul17-2002_d02957t.txt
./Post_Rate_Comm/Mitchell_6-17-Mit.txt`

This command gives all files over a certain size in increments of 512 bytes, so in this example, this is all the files in the `/.technial/government` directory over 51,200 bytes. This is useful if you want to look for the biggest files in a directory. 

### Example 2
`$ find -size 1k
./.git/config
./.git/description
./.git/HEAD
./.git/hooks/applypatch-msg.sample
./.git/hooks/commit-msg.sample
./.git/hooks/post-update.sample
./.git/hooks/pre-applypatch.sample
./.git/hooks/pre-merge-commit.sample
./.git/hooks/pre-receive.sample
./.git/info/exclude
./.git/logs/HEAD
./.git/logs/refs/heads/main
./.git/logs/refs/remotes/origin/HEAD
./.git/packed-refs
./.git/refs/heads/main
./.git/refs/remotes/origin/HEAD
./count-txts.sh
./README.md
./technical/plos/pmed.0020191.txt
./technical/plos/pmed.0020226.txt
./TestDocSearch.java
./thing.sh`

This example gives all files in a directory that are approximately one kilobyte in size, different from example one finding files over a certain size as this command is missing the + in front of the size designation. This is useful if you want to find all the files with a similar size in a directory.

## find -mtime/-mmin
### Example 1
`$ find . -mtime -1
./technical/911report/chapter-6.txt`

This command gives the files edited within the last day using `-mtime`. This is useful if you want to look at the files that you recently edited.

## Example 2
`$ find . -mmin -1
./technical/biomed/1471-213X-1-11.txt`

This command gives the files edited within the last minute using `mmin`, which is useful if you want to look at the most recently edited files.

## find . -empty
### Example 1
`$ find -empty
./.git/objects/info
./.git/refs/tags`

This command returns all empty files and directories, which is useful if you want to clean up your code and clear out any useless files.

### Example 2
`$ find -type d -empty
./.git/objects/info
./.git/refs/tags`

This command returns only empty directories because of the `-type d` distinction, which is useful if you want to find empty/unused directories.



