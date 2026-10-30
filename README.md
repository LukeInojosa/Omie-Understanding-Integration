# Omie-Understanding-Integration
Repositório para documentar sistema Omie a fim realizar integração

```mermaid
    erDiagram
        OrdemDeServico      ||--|{ ServicosPrestados: "tem"
        OrdemDeServico      }o--|| Cliente: "requisitante do servico"
        OrdemDeServico      ||--|{ Parcelas: "tipo de pagamento"
        OrdemDeServico      ||--o| produtosUtilizados: "eh utilizado"
        produtosUtilizados  ||--|{ produtoUtilizado: "utiliza"
        OrdemDeServico      ||--o| InformacoesAdicionais: possui
        produtoUtilizado    }o--|| Produto: "eh um"

        FornecedorDoProduto |o--|| Cliente: "eh um"
        FornecedorDoProduto }o--o{ Produto: "fornece" 
        
        ServicosPrestados   }o--|| Servico: " eh um" 
        ServicosPrestados   ||--o{ Impostos: "possui"

        ServicosPrestados {
            integer     nCodServico     "-> Servico"
            integer     nCodIntServico  "-> Servico"
            decimal     nQtde           "quantidade prestada do servico"
            string[1]   nTpDesconto     "Tipo de desconto do servico (P- percentual, V- Valor)"
            decimal     nValorDesconto
            decimal     nAliqDesconto
            string[1]   cNaoGerarFinanceiro "(S,N)"
        }

        Impostos {
            string[1] _cFixarISS   "indica se imposto foi alterado pelo usuario"
            decimal   nAliqISS     "aliquota do ISS"
            decimal   _nBaseISS    "base de calculo do ISS"
            decimal   _nValorISS   "valor do ISS"
        }

        produtoUtilizado{
            integer     nCodProdutoPU "-> Produto"
            integer     _nIdItemPU  "codigo interno da api"
            string[1]   cAcaoItemPU "A - alterar, E- excluir , I- Inserir"
            decimal     nQtdePU     "quantidade"
        }

        produtosUtilizados {
            string[3]   cAcaoProdUtilizados  "REM - remessa , EST - saida do estoque"
            string[20]  cCodCategRem         "Código da Categoria da Remessa"
        }

        FornecedorDoProduto{
            _ impostos
            _ categoriadeCompra
            _ codigoDoFornecedor
            _ CFOP
        }

        Produto {
            _ descricao
            integer     nCodProdutoPU "Codigo de Integeracao do Produto"
            integer     _nIdItemPU  "codigo interno da api"
            _ codigoEAN
            _ unidade
            _ precoUnitario
            _ codigoNCM
            _ definicaoDoProduto "(simples, kit ...)"
            _ ativo
        }

        Parcelas {
            integer     nParcela            "1,2,3"
            string[10]  dDtVenc             "data de vencimento da parcela"
            decimal     nValor              "valor da parcela"
            decimal     nPercentual         "percentual do valor do servico"
            string[100] meio_pagamento      "01 Dinheiro, 02 Cheque ..."
            string[1]   nao_gerar_boleto    "S para nao gerar boleto"
        }

        OrdemDeServico {
            string[60] cCodIntOS    "Codigo de Integracao"
            string[60] cCodIntCli   "-> Cliente"
            string[10] dDtPrevisao  "Data de Previsao"
            string[2]  cEtapa       "coluna do processo (01,02)"
            integer    nQtdeParc    "Quantidade de Parcelas"
            string[3]  cCodParc     "Condicao de Parcelamento"
            decimal    _nValorTotal  "Valor Total da Ordem de Servico"
        }
        InformacoesAdicionais {
            string[10] dDataRPS "data da RPS"
            string[10] _cNumRecibo "numero do recibo gerado"

        }
        Cliente {
            _ razaoSocial
            _ CNPJ-CPF
            _ nomeFantasia
            _ dadosBancarios
            _ contato
            _ endereco
            _ tags
        }

        Servico {
            string[20]  cCodServMun     "Codigo do Servico Municipal ou CNAE"
            string[20]  cCodServLC116   "Código do Serviço conforme Lei Complementar (LC 116)."
            integer     nCodServico     PK
            integer     nCodIntServico  "Codigo Integracao do Servico"
            text        cDescServ       "descricao do servico"
            string[9]   cNbs            "Codigo NBS do Servico"
            string[2]   cTribServ       "Tipo de Tributacao do Servico"
            string[1]   cRetemISS       "Retem ISS (S,N)"
            decimal     nValUnit        "valor unitario do servico"
        }
        
      
```
