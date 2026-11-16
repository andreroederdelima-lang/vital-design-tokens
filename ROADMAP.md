
## Nota de decisão (16/11/2026) — merge

- Merge liberado com CI verde, sem OK por PR, em todos os repos.
- Continua exigindo OK explícito do André: migração de banco; cobrança / pagamento / mensagem a cliente.
- Em plataforma.comissao.vital: CI verde + Codex sem findings.
- Em rescuedeck-producao: nenhum merge automático; todo merge exige OK explícito do André ou do Renann.
- Backup na mesma sessão antes de migração/deploy em produção.


## Nota de decisão (15/11/2026)

- Item travado: o executor pula e segue até a fase 8. Fases 9 a 14 só com pedido dele.
- Homologação: mesma VPS, em subdomínio, com banco separado.
- E-mail transacional: Resend. A chave ele fornece depois; até lá, envio desligado.
- Alerta de erro e de site fora do ar: Telegram.
- Backup diário fora da VPS: Cloudflare R2.
- Contato de plantão nos documentos de incidente: canal WhatsApp; deixe o número em branco para ele preencher.
