##### Backup das variáveis do usuário

```
Get-ChildItem Env: |
  Sort-Object Name |
  Select-Object Name, Value |
  ConvertTo-Json -Depth 3 |
  Out-File "$HOME\env-user.json" -Encoding UTF8
```

---

##### Backup das variáveis do sistema (admin)

```
Get-ChildItem Env: |
  Sort-Object Name |
  Select-Object Name, Value |
  ConvertTo-Json -Depth 3 |
  Out-File "$HOME\env-machine.json" -Encoding UTF8
```

---

##### Restaurar variáveis do usuário

```
$vars = Get-Content "$HOME\env-user.json" | ConvertFrom-Json

foreach ($v in $vars) {
  [Environment]::SetEnvironmentVariable($v.Name, $v.Value, "User")
}

Write-Host "Variáveis de usuário restauradas. Reinicie o terminal."
```

---
##### Restaurar variáveis do sistema (admin)

```
$vars = Get-Content "$HOME\env-machine.json" | ConvertFrom-Json

foreach ($v in $vars) {
  [Environment]::SetEnvironmentVariable($v.Name, $v.Value, "Machine")
}

Write-Host "Variáveis de sistema restauradas. Reinicie o Windows."
```
---

##### Antes de restaurar, salvar o PATH em um arquivo separado

```
$env:Path | Out-File "$HOME\path-backup.txt"
```
---
Lista de Programas para serem instalados

