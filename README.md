# azure-managed-identity
Demoing Azure Managed Identity (previously known also as MSI) with RBAC model for Azure DevOps

## Demoing Managed Identity in Azure App Service
$resource = "https://graph.microsoft.com"
$endpoint = $env:IDENTITY_ENDPOINT
$header = $env:IDENTITY_HEADER
$apiVersion = "2019-08-01"
$headers = @{ 'X-Identity-Header' = $header }
$url = "$($endpoint)?api-version=$apiVersion&resource=$resource"
echo $endpoint
echo $url

$response = Invoke-RestMethod -Method Get -Uri $url -Headers $headers
$response.access_token

(Invoke-WebRequest -Uri https://management.azure.com/subscriptions/0cb12691-4f8e-4a66-abab-4481e2f0517e/resourceGroups?api-version=2021-04-01 -Method GET -ContentType "application/json" -Headers @{ Authorization="Bearer $response.access_token"}).content
