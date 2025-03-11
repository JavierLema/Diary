---
tags: [RFE Sections]
title: Macro ReplaceFields
created: '2022-12-02T08:54:54.755Z'
modified: '2024-11-05T09:52:33.870Z'
---

# Macro ReplaceFields
### Uses a regular expresion:

`(\{(?<name>[\w\s:\-=]+)((?<sub>\[(?<j>[lLrR])?(?(j)(?<len>\d+)(,(?<start>\d+))?|(?<rstart>\d+)(-(?<rend>\d+))?)]))?\})|(\{\?(?<cond>\w+)\s*(?<exp>.*?)\?\}(?<true>.*?)(\{~\k<cond>\}(?<false>.*?))?\{\?\k<cond>\})|(\{#(?<table>\w+)\s*(?<query>.*?)#\}(?<fields>.*?)\{#\k<table>\})`

### Explanation with example:
- Three regular expresions concatenated with Logical OR operator
- Find any word start with '{' and ends with '}'

```
<style type="text/css">
    p
    {
    margin-top:0px;
    padding-top: 4px;
    margin-bottom:0px;
    padding-bottom:0px;
    }
    p  p
    {
    margin-top:0px;
    padding-top: 0px;
    margin-bottom:0px;
    padding-bottom:0px;
    }
</style>
<table style="width: 100%;">
    <tbody>
        <tr>
            <td style="width: 50%;" valign="top">{Client Logo Left}<br></td>
            <td align="right" style="width: 50%;" valign="center">&nbsp;{Client Logo Right}</td>
        </tr>
    </tbody>
</table>
<strong><span style="color: rgb(0, 0, 0);">{Alert Name}</span></strong><br>
<span style="color: rgb(0, 0, 0);">Run Time: {Alert Time}</span><br><br>
<span style="font-size: 16px; text-decoration: underline;"><strong>Search Results:</strong></span><br>
<br>
{#Items Items #}{?1 {Item_Title} ?}<strong><span style="color: rgb(0, 0, 0);">{Item_Title}</span></strong><br>
    {?1} <span style="color: rgb(0, 96, 255); font-size: 10px;">{Item_Pubname}<br>
    {?2 {Item_Author} ?}{Item_Author}<br>
    {?2} {Item_Pubdate}{?3 {Item_Volume} ?}, v:{Item_Volume}{?3}{?4 {Item_Issue} ?}, i:{Item_Issue}{?4}{?5 {Item_Pages} ?}, p:{Item_Pages}{?5}<br>
    </span>{?6 {Item_Abstract} ?}<span style="color: rgb(128, 128, 128); font-size: 10px;">
    <p>{Item_Abstract}</p>
    </span>{?6}<span style="color: rgb(1, 96, 255); font-size: 10px;">Order: <a href="{Item_Orderlink}">{Item_Orderlink}</a></span><br>
    <br>
{#Items}
```

#### Regular expresion matches:
- **{Client Logo Left}**, **{Client Logo Left}**: Defines in MacroValuesBase.cs
- **{Alert Name}**, **{Alert Time}**: Are defined in AlertMacroValues.cs
- **{#Items}**: MacroValues contains a virtual method to fill these items values: ResolveTable()... p.e. All data related with invoice: InvoiceMacroValues.cs

### Conditionals

- 15684 - Copyright Clearance Center Order {Order Id} - Panic

    ```{?eo {English Only}="yes" ?}Language: English Only{~eo}{?ep {English Preferred}="yes" ?}Language: English Preferred{?ep}{?eo}```

    The pseudocode to interpreted this macro:
    {English Only} => case "english only": value = AsYesNo(Order.SpecInstructEnglishOnly); break;
    {English Preferred} => case "english only": value = AsYesNo(Order.SpecInstructEnglishOnly); break;
    if (Order.SpecInstructEnglishOnly)
        Console.WriteLine('Language: English Only')
    else if (Order.SpecInstructEnglishOnly)
        Console.WriteLine('Language: English Preferred')



SET STATISTICS TIME ON
