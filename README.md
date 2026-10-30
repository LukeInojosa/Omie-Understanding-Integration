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
            integer     codigo_cliente_omie         "codigo do cliente no omie"
            string[60]  codigo_cliente_integracao   "codigo de integracao"
            string[60]  razao_social
            string[20]  cnpj_cpf
            string[100] nome_fantasia
            string[5]   telefone1_ddd
            string[15]  telefone1_numero
            string[100] conato                      "nome do contato"
            string[60]  endereco
            string[60]  endereco_numero
            string[60]  bairro
            string[60]  complemento
            string[2]   estado                      "sigla do estado"
            string[40]  cidade
            string[10]  cep
            string[4]   codigo_pais
            string[1]   pesquisar_cep               "se S, o sistema preenche logradouro, bairro e cidade, conforme dados do cep"
            string[500] email
            string[7]   cidade_ibge
            string[1]   inativo                     "(S,N)"
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
