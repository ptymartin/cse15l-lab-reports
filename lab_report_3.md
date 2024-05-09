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
```
grep -c "option" 911report/*.txt
911report/chapter-1.txt:0
911report/chapter-10.txt:6
911report/chapter-11.txt:7
911report/chapter-12.txt:3
911report/chapter-13.1.txt:2
911report/chapter-13.2.txt:0
911report/chapter-13.3.txt:2
911report/chapter-13.4.txt:10
911report/chapter-13.5.txt:5
911report/chapter-2.txt:1
911report/chapter-3.txt:29
911report/chapter-5.txt:1
911report/chapter-6.txt:22
911report/chapter-7.txt:0
911report/chapter-8.txt:0
911report/chapter-9.txt:2
911report/preface.txt:0
```
Returns the count of how many times the pattern "option" appears in each `.txt` file in `technical/911report` next to the relative path of the file.


```
grep -c "other" government/About_LSC/*.txt
government/About_LSC/CONFIG_STANDARDS.txt:9
government/About_LSC/Comments_on_semiannual.txt:9
government/About_LSC/LegalServCorp_v_VelazquezDissent.txt:15
government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt:12
government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt:4
government/About_LSC/ODonnell_et_al_v_LSCdecision.txt:1
government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt:23
government/About_LSC/Progress_report.txt:34
government/About_LSC/Protocol_Regarding_Access.txt:13
government/About_LSC/Special_report_to_congress.txt:33
government/About_LSC/State_Planning_Report.txt:76
government/About_LSC/State_Planning_Special_Report.txt:15
government/About_LSC/Strategic_report.txt:31
government/About_LSC/commission_report.txt:62
government/About_LSC/conference_highlights.txt:4
government/About_LSC/diversity_priorities.txt:16
government/About_LSC/reporting_system.txt:17
```
Returns the count of how many times the pattern "other" appears in each `.txt` file in `technical/government/About_LSC` next to the relative path of the file.


### Option 2: `-i`

```
grep --color -i "intEgratEd" 911report/*.txt
911report/chapter-12.txt:                need to fashion a broad, integrated plan to stop the next generation of terrorists?
911report/chapter-12.txt:                have been wrong. It means those choices must be integrated with America's message of
911report/chapter-12.txt:            Since 9/11, significant improvements have been made to create an integrated watchlist
911report/chapter-12.txt:                official put it34-new insights into terrorist travel have not yet been integrated
911report/chapter-12.txt:                Recommendation: The U.S. border security system should be integrated
911report/chapter-12.txt:                    development of an integrated system, which in turn can become part of the wider
911report/chapter-12.txt:                    travelers. It should be integrated with the system that provides benefits to
911report/chapter-12.txt:            Despite congressional deadlines, the TSA has developed neither an integrated
911report/chapter-13.1.txt:                whole. Integrated all-source analysis should also inform and shape strategies to
911report/chapter-13.1.txt:                    agencies, not the joint mission. The importance of integrated, allsource
911report/chapter-13.1.txt:                    became more integrated.
911report/chapter-13.1.txt:                    CIA's experts should be integrated into the military's training, exercises, and
911report/chapter-13.1.txt:                Recommendation: A specialized and integrated national security
911report/chapter-13.3.txt:            80. "According to the 2002 Integrated Postsecondary Education Data System statistics,
911report/chapter-13.4.txt:                integrated al Qida-Afghan- Pakistan paper," June 30, 2001. For State's view, see DOS
911report/chapter-13.5.txt:                would offer an integrated depiction of groups like al Qaeda or Hezbollah worldwide,
911report/chapter-3.txt:                said: First, we will use our new integrated approach to intensify the fight against
911report/chapter-3.txt:                consider an integrated policy toward terrorism, which might range from identifying
911report/chapter-6.txt:                But the pieces were coming together for an integrated policy dealing with al Qaeda,
911report/chapter-9.txt:                911 operators and FDNY dispatch were not adequately integrated into the emergency
911report/chapter-9.txt:            It is also clear, however, that the response operations lacked the kind of integrated
911report/chapter-9.txt:                would have been in the Twin Towers if there had been an integrated response, or what
911report/chapter-9.txt:                creates. The experience of the military suggests that integrated into such a
```
Returns the lines of text containing the case-insensitive pattern "integrated" in each `.txt` file in `technical/911report` next to the relative path of the file.

```
grep --color -i "ComPreHensIve" government/About_LSC/CONFIG_STANDARDS.txt
Configuration Standards -- presents in one place a comprehensive
other equal justice stakeholders3 to develop comprehensive,
comprehensive set of strategies employed to promote the creation
and sustainability of comprehensive, integrated state civil equal
comprehensive, integrated delivery system. This duty can be
eligible clients throughout the state within a comprehensive,
effective, culturally relevant, systematic and comprehensive
goals and objectives of a comprehensive, integrated and
```
Returns the lines of text containing the case-insensitive pattern "comprehensive" in `government/About_LSC/CONFIG_STANDARDS.txt`.

### Option 3: `-l`

```
grep -l "options" 911report/*.txt
911report/chapter-10.txt
911report/chapter-11.txt
911report/chapter-13.1.txt
911report/chapter-13.3.txt
911report/chapter-13.4.txt
911report/chapter-13.5.txt
911report/chapter-2.txt
911report/chapter-3.txt
911report/chapter-6.txt
```
Returns the relative paths of the `.txt` files containing the pattern "options" at least one time in `technical/911report`

```
grep -l "other" government/About_LSC/*.txt
government/About_LSC/CONFIG_STANDARDS.txt
government/About_LSC/Comments_on_semiannual.txt
government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
government/About_LSC/ODonnell_et_al_v_LSCdecision.txt
government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
government/About_LSC/Progress_report.txt
government/About_LSC/Protocol_Regarding_Access.txt
government/About_LSC/Special_report_to_congress.txt
government/About_LSC/State_Planning_Report.txt
government/About_LSC/State_Planning_Special_Report.txt
government/About_LSC/Strategic_report.txt
government/About_LSC/commission_report.txt
government/About_LSC/conference_highlights.txt
government/About_LSC/diversity_priorities.txt
government/About_LSC/reporting_system.txt
```
Returns the relative paths of the `.txt` files containing the pattern "other" at least one time in `technical/government/About_LSC`

### Option 4: `-m`

```
grep --color -m 1 "options" 911report/*.txt
911report/chapter-10.txt:                officer, quickly researched the options and, sometime around 10:20, identified
911report/chapter-11.txt:                so might the range of options for a president--had they been informed of these
911report/chapter-13.1.txt:                and seeks help with it. When they act jointly, the problem and options for action
911report/chapter-13.3.txt:                options the CIA could be pursuing against Bin Ladin: paramilitary or sabotage
911report/chapter-13.4.txt:                options- investments that pay off only when a stock drops in price-surged in the
911report/chapter-13.5.txt:                limited options immediately available in Afghanistan and the lack of ground options.
911report/chapter-2.txt:                factions. Bin Ladin apparently kept his options open, maintaining contacts with
911report/chapter-3.txt:            However, it also may have lessened the diversity of military advice and options
911report/chapter-6.txt:                possibilities to a set of 13 options within the Operation Infinite Resolve
```
Returns the lines of the first n matches of the pattern "options" in all the `.txt` files in `technical/911report` next to the file's relative path. In this case, n is specified to be 1.


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
