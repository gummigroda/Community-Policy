# Azure Log Analytics for Windows VM's - Without a Tag

This custom Azure Policy will enable the Log Analytics Agent on all Windows VMs WITHOUT the specified "tagName : [tagValue]" and connect them to a existing Log Analytics Workspace.  

Additional parameters that are required for this policy include:
* Resource ID of the Log Analytics Workspace to connect the vm's to.

Parameters that are optional:
* Exclusion tag name (defaults to: 'SkipMonitor')
* Exclusion tag value (defaults to: 'true', 'yes' or 1)
* List of images to include in the definition
* Effect of the policy

## Try in Portal

[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fcommunity-policy%2Fmaster%2Fpolicies%2FMonitoring%2deploy-oms-agent-windows-vm-without-tag%2Fazurepolicy.json)

## Try with PowerShell

```powershell

$Scope = (Get-AzContext).Subscription.Id
$Properties = @{
    Name = 'deploy-oms-agent-windows-vm-without-tag'
    DisplayName = 'Enable Log Analytics on Windows VMs without a given tag to an existing Log Analytics Workspace'
    Description = 'Enable Log Analytics on Windows VMs by connecting them to an existing central Log Analytics Workspace. You can optionally exclude virtual machines containing a specified tag to control the scope of assignment.'
    Policy = 'https://raw.githubusercontent.com/Azure/Community-Policy/master/Policies/Monitoring/deploy-oms-agent-windows-vm-without-tag/azurepolicy.rules.json'
    Parameter = 'https://raw.githubusercontent.com/Azure/Community-Policy/master/Policies/Monitoring/deploy-oms-agent-windows-vm-without-tag/azurepolicy.parameters.json'
    Mode = 'All'
}

$PolicyDefinition = New-AzPolicyDefinition @Properties

New-AzPolicyAssignment -Name $Properties.Name ` 
    -DisplayName $Properties.DisplayName ` 
    -Scope <scope> `
    -PolicyDefinition $PolicyDefinition ` 
    -effect <AuditIfNotExists|Disabled> ` 
    -logsEnabled <True|False>

```
