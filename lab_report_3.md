# Lab Report 3 - Bugs and Commands
---
## Part 1 - Bugs
I chose the method reverseInPlace in the ArrayExamples class: 
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```

A failure inducing input on this method:
```
@Test
public void testReverseInPlaceFull() {
  int[] input1 = {1, 2, 3};
  ArrayExamples.reverseInPlace(input1);
  int[] expected = {3, 2, 1};

  assertArrayEquals(expected, input1);
}
```

An input that does not induce failure:
```
@Test 
public void testReverseInPlace() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```

Output of running the two tests above:
![Tests Output](test_outputs.png)

The code before and after being fixed:
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
```
static void reverseInPlace(int[] arr) {
  int[] temp = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    temp[i] = arr[arr.length - i - 1];
  }
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = temp[i];
  }
}
```

The issue with the original method was trying to reverse the array without storing the values of the original array. This means that when a value is written over, the original can no longer be placed in its correct place. The fixed code creates an empty array of the same size, and then reverses the values by copying in reverse order to the new array, which allows for all the original values to be kept.

---
## Part 2 - Researching commands
Command: `grep`

### Option 1: `-c`
![Count example 1](grep-c1.png)
Returns the count of how many times the pattern "option" appears in each `.txt` file in `technical/911report` next to the relative path of the file.


![Count example 2](grep-c2.png)
Returns the count of how many times the pattern "other" appears in each `.txt` file in `technical/government/About_LSC` next to the relative path of the file.


### Option 2: `-i`

![Case insensitive example 1](grep-i1.png)
Returns the lines of text containing the case-insensitive pattern "integrated" in each `.txt` file in `technical/911report` next to the relative path of the file.

![Case insensitive example 2](grep-i2.png)
Returns the lines of text containing the case-insensitive pattern "comprehensive" in `government/About_LSC/CONFIG_STANDARDS.txt`.

### Option 3: `-l`

![File names example 1](grep-l1.png)
Returns the relative paths of the `.txt` files containing the pattern "options" at least one time in `technical/911report`

![File names example 2](grep-l2.png)
Returns the relative paths of the `.txt` files containing the pattern "other" at least one time in `technical/government/About_LSC`

### Option 4: `-m`

![Stop early example 1](grep-m1.png)
Returns the lines of the first n matches of the pattern "options" in all the `.txt` files in `technical/911report` next to the file's relative path. In this case, n is specified to be 1.

![Stop early example 2](grep-m2.png)

```
grep --color -m 1 "other" government/About__SC/*.txt
government/About_LSC/CONFIG_STANDARDS.txt:and territory to work with one another and with a broad spectrum of
government/About_LSC/Comments_on_semiannual.txt:providing models and inspiration for others. All 18 states improved
government/About_LSC/LegalServCorp_v_VelazquezDissent.txt:involve an effort to amend or otherwise challenge existing law in
government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt:funds and other public or private sources. The grantee
government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt:in an effort to amend or otherwise challenge existing welfare law.
government/About_LSC/ODonnell_et_al_v_LSCdecision.txt:*We note that three other circuits have concluded that rational
government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt:people who could not otherwise afford legal aid. As did many of you
government/About_LSC/Progress_report.txt:me it demonstrates another very important point. It shows that a
government/About_LSC/Protocol_Regarding_Access.txt:any of LSC's rights to documents and other information and does not
government/About_LSC/Special_report_to_congress.txt:quality legal assistance to those who would otherwise be unable to
government/About_LSC/State_Planning_Report.txt:services delivery system, created in another time and place, didn't
government/About_LSC/State_Planning_Special_Report.txt:legal assistance to those who would otherwise be unable
government/About_LSC/Strategic_report.txt:in this great country, we began to focus on other initiatives that
government/About_LSC/commission_report.txt:housing, transportation and other employment rights under the
government/About_LSC/conference_highlights.txt:sharing how programs can build bridges with other equal justice
government/About_LSC/diversity_priorities.txt:Focusing on broad aspects of diversity - including, among others,
government/About_LSC/reporting_system.txt:that they work cooperatively with other groups to address the needs
```

Returns the lines of the first n matches of the pattern "other" in all the `.txt` files in `government/About_LSC` next to the file's relative path. In this case, n is specified to be 1.

All options were found using the integrated `man` command
