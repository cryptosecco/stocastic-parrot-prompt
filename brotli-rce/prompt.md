# Usi agenti AI? Sei a rischio: il prompt per metterti al sicuro

- URL: https://stocasticparrot.ai/sicurezza/brotli-rce/
- Aggiornato: 2026-11-01

```text
Sei un assistente tecnico incaricato di verificare e mettere in sicurezza questa macchina rispetto a CVE-2026-111497 (scrittura fuori dai limiti nel decoder Brotli di Google, incluso in Node.js e Bun) e alle altre 9 vulnerabilità della security release Node.js del 21 ottobre 2026.
Esegui i passaggi in ordine, documenta ogni output e riassumi lo stato finale. Prima di ogni aggiornamento mostra il comando e aspetta il mio ok.

1. Inventario completo
• Mostra: node -v, which -a node (su Windows: where node) e la versione di ogni node trovato; bun -v e which -a bun; claude --version e claude doctor
• Cerca altri runtime: installazioni Node/Bun gestite da nvm, fnm, asdf, Volta o simili
• Identifica i tool AI e gli agenti presenti (Claude Code, Cursor, Codex, Aider, Open Interpreter, Continue, Hermes Agent ecc.) e verifica se usano un runtime incorporato: cerca le cartelle con un node o un bun propri
• Cerca gli eseguibili single-file (Node SEA, bun build --compile): incorporano il runtime e vanno ricompilati
• Controlla le immagini Docker: docker images | grep -E 'node|bun'
• Su Linux controlla la versione del pacchetto brotli di sistema: su Debian e Ubuntu Node usa quella

2. Aggiornamento Node.js
• Porta il Node di sistema e tutte le installazioni gestite alle versioni corrette: ≥ 22.23.4 sulla linea 22, ≥ 24.22.1 sulla 24, ≥ 26.12.1 sulla 26
• Le linee 25, 23, 21, 20 e precedenti non ricevono la correzione: proponi la migrazione a una linea supportata
• Usa il metodo adatto a come è installato (nvm, Homebrew, NodeSource, winget, installer ufficiale)
• Riavvia i processi Node attivi

3. Aggiornamento Bun e Claude Code
• Aggiorna Bun a ≥ 1.4.4 (bun upgrade, o brew upgrade bun se viene da Homebrew)
• Claude Code deve essere ≥ 2.1.308. Installazione nativa: claude update. npm: npm install -g @anthropic-ai/claude-code@latest. Homebrew: brew upgrade claude-code (o claude-code@latest). WinGet: winget upgrade Anthropic.ClaudeCode. apt, dnf, apk: aggiorna il pacchetto claude-code
• Aggiorna gli altri tool AI che includono un runtime proprio, dal loro canale ufficiale

4. Docker e ambienti containerizzati
• Segnala le immagini basate su versioni vulnerabili
• Indica i comandi per aggiornarle: docker pull node:24 (o il tag in uso), poi docker build --pull e nuovo deploy. Riavviare il container vecchio non basta

5. Pacchetti e sistema
• Aggiorna i package manager globali (npm, yarn, pnpm), se presenti
• Suggerisci l’aggiornamento del sistema operativo (apt, brew, winget, Windows Update, aggiornamenti di macOS)
• Nota: npm audit non copre questo bug, che è nel runtime e non nei pacchetti

6. Verifica finale e raccomandazioni
• Riesegui i controlli di versione su ogni runtime trovato
• Conferma che non restino runtime vulnerabili attivi
• Indica le azioni manuali rimaste
• Suggerisci le pratiche minime: isolare gli agenti quando possibile, non fare fetch di contenuti non fidati senza controlli, tenere attivi gli aggiornamenti automatici, non eseguire PoC trovati online

Non eseguire operazioni distruttive: niente disinstallazioni o cancellazioni. Alla fine riporta una tabella (runtime, percorso, versione prima e dopo, stato) e separa ciò che hai aggiornato da ciò che richiede intervento umano.
```
