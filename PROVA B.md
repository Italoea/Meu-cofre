

dia/mês/2025-hr:min:seg

echo "+%d/%m/%Y-%H:%M:%S"

uma função que recebe duas listas e concatena as duas, no caso junta as duas

Import-Module ActiveDirectory

$OU = "OU=ITNSA,OU=WSC,DC=worldskills,DC=org"

$pwd = ConvertTo-SecureString "Skill39@" -AsPlainText -Force

1..100 | Foreach-Object {

$user="user$

New-ADUser -Name $user -SamAccountName $user AccountPassword $pwd -Enabled $true -Path $OU

Add-GroupMember -Identity Skill -Members $user

}

Get-WindowsFeature --AD-Domain-Services

APONTAR A ROTA PARA ELE MESMO 10.0.0.2 E COLOCAR ENDEREÇO ESTATICO

SEPARA POR UMA CATEGORIA OS SERVIÇOS

FACIL

MÉDIO

DIFICIL

MARCAR SERVIÇOS QUE DEMORAM PRA CONFIGURAR

Autorização Necessária

netsh advfirewall set allprofiles state off --> PRA DESKIGAR O FIREWALL DO CORE

 Install-WindowsFeature RemoteAccess

 Install-WindowsFeature Routing

Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools

Install-RemoteAccess -VpnType VpnS2S

NO WINDOWS CORE BR-R PARA CONFIGURAR A VPN SITE TO SITE

Add-VpnS2SInterface `

  -Name "VPN‑To‑BranchA" `

  -Destination 1.1.1.2 ` # IP do outro servidor

  -Protocol IKEv2 `

  -AuthenticationMethod PSKOnly `

  -SharedSecret "ChaveSegura123!" `

  -IPv4Subnet 10.10.0.0/24:100 # Sub‑rede da outra ponta