
# Configurando DHCP no Cliente Linux

Para configurar um cliente Linux para obter um endereço IP automaticamente via DHCP, edite o arquivo `/etc/network/interfaces`.

## Passos:

1. **Abra o arquivo de configuração**:
```
sudo nano /etc/network/interfaces
```

2. **Adicione a seguinte configuração para ativar o DHCP na interface desejada** (substitua `eth0` pelo nome correto da interface de rede):
```
auto eth0
iface eth0 inet dhcp
```

3. **Salve e saia** do editor (no Nano, pressione `CTRL+X`, `Y` e `Enter`).

4. **Reinicie a interface de rede para aplicar as mudanças**:
```
sudo systemctl restart networking
```

Ou use o comando:

```
sudo ifdown eth0 && sudo ifup eth0
```

5. **Verifique se o IP foi obtido via DHCP**:
```
ip addr show eth0
```


# Configurando IP Estático no Cliente Linux

Se você deseja configurar um endereço IP estático, siga os passos abaixo.

## Passos:

1. **Abra o arquivo de configuração**:
    
    ```
    sudo nano /etc/network/interfaces
    ```
    
2. **Adicione a seguinte configuração** (substitua os valores conforme necessário):
    
    ```
    auto eth0
    iface eth0 inet static
        address 192.168.1.100
        netmask 255.255.255.0
        gateway 192.168.1.1
        dns-nameservers 8.8.8.8 8.8.4.4
    ```
    
3. **Salve e saia** do editor (no Nano, pressione `CTRL+X`, `Y` e `Enter`).
    
4. **Reinicie a interface de rede para aplicar as mudanças**:
    
    ```
    sudo systemctl restart networking
    ```
    
    Ou use o comando:
    
    ```
    sudo ifdown eth0 && sudo ifup eth0
    ```
    
5. **Verifique a configuração da rede**: