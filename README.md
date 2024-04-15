## Repositório de Diagramas do Projeto

**Descrição:**

Este repositório armazena os diagramas do projeto, incluindo:

* Diagramas de classes
* Diagramas de sequência
* Diagramas ER

**Objetivo:**

O objetivo deste repositório é centralizar os diagramas do projeto, facilitando o acesso e a compreensão da arquitetura do sistema.

**Estrutura do Repositório:**

* **Diagramas de Classes:**
    * Pasta `classes`
    * Cada diagrama em um arquivo `.png` ou `.svg`
    * Nome do arquivo deve ser descritivo do diagrama
* **Diagramas de Sequência:**
    * Pasta `sequencia`
    * Cada diagrama em um arquivo `.png` ou `.svg`
    * Nome do arquivo deve ser descritivo do diagrama
* **Diagramas ER:**
    * Pasta `er`
    * Cada diagrama em um arquivo `.png` ou `.svg`
    * Nome do arquivo deve ser descritivo do diagrama

**Diagrama de Classes:**

```mermaid
classDiagram
    class Usuario {
        -usuarioID: int
        -nome: string
        -email: string
        -telefone: string
        -ra: string
        -tipoUsuario: string
        -permissao: string
        +realizarOrdem(ordem: Ordem)
        +fazerInscricao(inscricao: Inscricao)
        +submeterTrabalho(submissao: Submissao)
        +receberCertificado(certificado: Certificado)
        +editarPerfil()
        +alterarSenha()
        +verificarPermissao(permissao: string): bool
        +bloquearUsuario()
        +desbloquearUsuario()
        +resetarSenha()
        +enviarNotificacao(mensagem: string)
    }

    class Evento {
        -eventoID: int
        -nome: string
        -descricao: string
        -dataInicio: datetime
        -dataTermino: datetime
        -modalidade: string
        -limiteParticipantes: int
        +adicionarAtividade(atividade: Atividade)
        +emitirIngresso(ingresso: Ingresso)
        +gerarCertificado(certificado: Certificado)
        +editarDetalhes()
        +cancelarEvento()
        +listarInscritos(): List<Usuario>
        +listarAtividades(): List<Atividade>
        +listarIngressos(): List<Ingresso>
        +listarCertificados(): List<Certificado>
        +definirLimiteParticipantes(limite: int)
        +alterarModalidade(modalidade: string)
        +verificarDisponibilidade(): bool
    }

    class Atividade {
        -atividadeID: int
        -nome: string
        -descricao: string
        -dataHoraInicio: datetime
        -dataHoraTermino: datetime
        -valor: decimal
        -quantidadeVagas: int
        -local: Local
        +inscreverParticipante(inscricao: Inscricao)
        +receberSubmissao(submissao: Submissao)
        +editarDetalhes()
        +cancelarAtividade()
        +listarInscritos(): List<Usuario>
        +listarSubmissoes(): List<Submissao>
        +definirQuantidadeVagas(vagas: int)
        +definirValor(valor: decimal)
        +definirLocal(local: Local)
        +verificarDisponibilidade(): bool
    }

    class Local {
        -localID: int
        -nome: string
        -descricao: string
        -capacidade: int
        -equipamentos: string
        +reservarLocal(atividade: Atividade): bool
        +liberarLocal(atividade: Atividade)
        +listarReservas(): List<Atividade>
        +editarDetalhes()
        +definirCapacidade(capacidade: int)
        +adicionarEquipamento(equipamento: string)
        +removerEquipamento(equipamento: string)
    }

    class Ordem {
        -ordemID: int
        -dataCriacao: datetime
        -valorTotal: decimal
        -formaPagamento: string
        -statusPagamento: string
        -codigoPagamento: string
        +adicionarIngresso(ingresso: Ingresso)
        +removerIngresso(ingresso: Ingresso)
        +realizarPagamento(): bool
        +cancelarOrdem()
        +listarIngressos(): List<Ingresso>
        +calcularValorTotal(): decimal
        +gerarCodigoPagamento(): string
        +verificarStatusPagamento(): string
    }

    class Ingresso {
        -ingressoID: int
        -inscricaoID: int
        -codigoIngresso: string
        -dataEmissao: datetime
        -evento: Evento
        -atividade: Atividade
        +validarIngresso(): bool
        +emitirIngresso(evento: Evento, atividade: Atividade)
        +cancelarIngresso()
        +gerarCodigoIngresso(): string
        +verificarValidade(): bool
    }

    class Inscricao {
        -inscricaoID: int
        -usuarioID: int
        -atividadeID: int
        -valorTotal: decimal
        -formaPagamento: string
        -statusPagamento: string
        +adicionarAtividade(atividade: Atividade)
        +removerAtividade(atividade: Atividade)
        +realizarPagamento()
        +cancelarInscricao()
    }

    class Certificado {
        -certificadoID: int
        -atividadeID: int
        -usuarioID:int
        -dataEmissao: datetime
        -codigoVerificacao: string
        +validarCertificado(): bool
        +gerarCodigoVerificacao(): string
        +enviarCertificadoParticipante(participante: Usuario)
        +emitirCertificado(evento: Evento, participante: Usuario)
        +cancelarCertificado(certificadoID: int)
    }

    class Submissao {
        -submissaoID: int
        -tituloTrabalho: string
        -descricao: string
        -arquivo: blob
        -dataSubmissao: datetime
        -status: string
        +avaliarSubmissao()
        +definirStatus(status: string)
        +adicionarFeedback(feedback: string)
        +enviarNotificacaoAutor(mensagem: string)
        +validarFormato(): bool
        +verificarPrazo(): bool
    }

    Usuario ..> Ordem
    Usuario ..> Inscricao
    Usuario ..> Submissao
    Usuario ..> Certificado
    Evento ..> Atividade
    Evento ..> Ingresso
    Evento ..> Inscricao
    Evento ..> Submissao
    Evento ..> Certificado
    Atividade ..> Inscricao
    Atividade ..> Submissao
    Atividade ..> Local
    Ordem ..> Ingresso
    Inscricao ..> Atividade

    end
```

**Diagrama de Sequência:**

```mermaid
sequenceDiagram
    participant Usuario
    participant Sistema
    autonumber
    Usuario->Sistema: Realizar login (email, senha)
    Sistema->Usuario: Validar login (autenticação)
    alt Autenticação bem sucedida
        Sistema->Usuario: Exibir tela inicial
    else Autenticação falhou
        Sistema->Usuario: Exibir mensagem de erro
        Usuario->Sistema: Tentar novamente
    end
```

**Diagrama ER:**

```mermaid
erDiagram
   Usuario ||--o{ Ordem : realiza
   Usuario ||--o{ Inscricao : faz
   Usuario ||--o{ Submissao : submete
   Usuario ||--o{ Certificado : recebe
   Evento ||--|{ Atividade : inclui
   Evento ||--o{ Ingresso : emite
   Evento ||--|| Inscricao : recebe
   Evento ||--|| Submissao : recebe
   Evento ||--|| Certificado : gera
   Atividade ||--o{ Inscricao : inclui
   Atividade ||--o{ Submissao : recebe
   Atividade ||--|| Local : realizada_em
   Ordem ||--o{ Ingresso : inclui
   Inscricao ||--o{ Atividade : inscreve

   Usuario {
       int usuarioID
       string nome
       string email
       string telefone 
       string ra
       string tipoUsuario
       string permissao
   }

   Evento {
       int eventoID
       string nome
       string descricao
       datetime dataInicio
       datetime dataTermino
       string modalidade
       int limiteParticipantes
   }

   Atividade {
       int atividadeID
       string nome
       string descricao
       datetime dataHoraInicio
       datetime dataHoraTermino
       decimal valor
       int quantidadeVagas
   }

   Local {
       int localID
       string nome
       string descricao
       int capacidade
       string equipamentos
   }

   Ordem {
       int ordemID
       datetime dataCriacao
       decimal valorTotal
       string formaPagamento
       string statusPagamento
       string codigoPagamento
   }

   Ingresso {
       int ingressoID
       int inscricaoID
       string codigoIngresso
       datetime dataEmissao
   }

   Inscricao {
       int inscricaoID
       decimal valorTotal
       string formaPagamento
       string statusPagamento
   }

   Certificado {
       int certificadoID
       datetime dataEmissao
       string codigoVerificacao
   }

   Submissao {
       int submissaoID
       string tituloTrabalho
       string descricao
       blob arquivo
       datetime dataSubmissao
       string status
   }

    end
```
