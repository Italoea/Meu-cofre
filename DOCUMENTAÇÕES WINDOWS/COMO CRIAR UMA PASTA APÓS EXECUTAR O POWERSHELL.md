

# ABRA O POWERSHEL E DÊ O COMANDO:


```
notepad $profile.AllUsersAllHosts
```

## IRÁ ABRIR UM NOTEPAD E LÁ VOCÊ COLOCARÁ SEU SCRIPT PARA CRIAR A PASTA

```
$data = Get-Date -Format "yyyy-MM-dd"
$pasta = "C:\Log\PowerShell$data"

if (!(Test-Path $pasta)) {
    New-Item -Path $pasta -ItemType Directory | Out-Null
}
```

### ESSE SCRIPT CRIA UMA PASTA NO DISCO "C:" COM O NOME "Log" E DENTRO DELA CRIA OUTRA PASTA COM O NOME "Powershell2025-07-23"

##### PARA VERIFICAR QUAIS PROFILES QUE EXISTEM DÊ O COMANDO:

```
$PROFILE | Get-Member
```


