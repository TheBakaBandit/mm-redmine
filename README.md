# mm-redmine

WIP - Redmine PowerShell module

## Login

```ps1
# Login to redmine using your key: My account -> API access key
# Must have Administration -> Settings -> API -> [x] Enable REST web service
Initialize-RedmineSession -Url 'https://redmine...' -Key '<key>'
```

## Projects

```ps1

# Get all projects
Get-RedmineProject | Format-Table

# Get project by name
Get-RedmineProject -Name hmr
```

## Issues

```ps1

#Get single issue
Get-RedmineIssue -Id 112 -Include watchers

# Get all issues

Get-RedmineIssue

# Get project issues and show them in table
$filter = New-RedmineIssueFilter -ProjectId $project.id
$issues = Get-RedmineIssue -Filter $filter
$htAuthor = @{ N='author'; E={$_.author.name} }
$issues | Format-Table subject, $htAuthor, created_on, start_date, due_date

# Filter issues by custom field by the name 'Level'
$f = New-RedmineIssueFilter -ProjectId $p.id
$cf = Get-RedmineIssue -Filter $filter -Limit 1 | % custom_fields
$levelId = Get-RedmineCustomFieldId $cf Level
$filter = New-RedmineIssueFilter -ProjectId $p.id -CustomFields @{ levelId = 'Senior' }
Get-RedmineIssue -Filter $filter
```
