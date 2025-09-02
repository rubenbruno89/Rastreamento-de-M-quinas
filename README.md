# 🖥️ Script em Lote — Rastreamento de Máquinas

Este script em lote (`.bat`) foi desenvolvido para **Windows** e permite verificar se uma máquina na rede está online e, em caso positivo, listar as sessões ativas na máquina usando `qwinsta`.

---

## 📌 Funcionalidades
- Solicita o **host ou IP** da máquina a ser rastreada.  
- Faz um **ping** para checar se a máquina está ativa.  
- Se o host responder:  
  - Executa `qwinsta` remotamente para listar as sessões abertas.  
  - Exibe se existe sessão **console** (usuário logado diretamente na máquina).  
- Se o host não responder:  
  - Informa que a máquina está fora da rede ou desligada.  

---

## ⚙️ Requisitos
- **Windows** com suporte a:
  - `ping` (nativo do sistema).  
  - `qwinsta` (comando disponível em versões Pro/Enterprise do Windows).  
- Permissão de rede para consultar sessões remotas.  

---

## ▶️ Como usar
1. Salve o código abaixo como `rastreamento_maquinas.bat`.  
2. Execute o script (`duplo clique` ou via `cmd`).  
3. Informe o **host/IP** da máquina que deseja verificar.  

---

## 📂 Script
```bat
@echo off
cls
echo ----------------------------------------------------------------
echo  RASTREAMENTO DE MAQUINAS
echo ----------------------------------------------------------------
:loop
echo.
set /p host=Digite o host ou ip da maquina:
ping %host% -v -a -n 2 | find "TTL" >> resul.txt
if errorlevel 1 (
    echo %host% esta fora da rede ou  desligado, tente mais tarde.
) else (
    echo %host% esta online
    qwinsta /SERVER:%host% >> resul.txt
    type resul.txt | findstr /C:"console"
    del resul.txt
)
goto loop
```

---

## 📌 Observações
- O script roda em **loop infinito**, permitindo testar várias máquinas sem reiniciar.  
- A sessão **console** indica se há um usuário logado localmente na máquina.  
- Pode ser útil para administradores de rede monitorarem estações de trabalho.  

---

✍️ Criado para facilitar o rastreamento rápido de máquinas na rede.
