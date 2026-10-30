# Omie-Understanding-Integration
Repositório para documentar sistema Omie a fim realizar integração

```mermaid
    erDiagram
        OrdemDeServico ||--|{ ServicosPrestados: "tem"
        OrdemDeServico }o--|| Cliente: "requisitante do servico"
        OrdemDeServico ||--|{ Parcelas: "tipo de pagamento"
        OrdemDeServico ||--o{ ProdutoDaOrdem: "eh utilizado"
        OrdemDeServico ||--o| InformacoesAdicionais: possui
        ProdutoDaOrdem }o--|| Produto: "eh um"

        FornecedorDoProduto |o--|| Cliente: "eh um"
        FornecedorDoProduto }o--o{ Produto: "fornece" 
        
        ServicosPrestados }o--|| Servico: " eh um" 
        ServicosPrestados ||--o{ Impostos: "possui"

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

        ProdutoDaOrdem {
            _ quantidade
            _ localDoEstoque
            _ valorUnitario
            _ desconto
            _ tabelaDePreco
            _ Acao "(Gerar Remessa, Gerar Pedido de Venda)"
        }

        FornecedorDoProduto{
            _ impostos
            _ categoriadeCompra
            _ codigoDoFornecedor
            _ CFOP
        }

        Produto {
            _ descricao
            _ codigoDoProduto
            _ codigoEAN
            _ unidade
            _ precoUnitario
            _ codigoNCM
            _ definicaoDoProduto "(simples, kit ...)"
            _ ativo
        }

        Parcelas {
            _ percentualDaParcela "em relacao valorServicos + valorProdutos"
            _ valorDaParcela
            _ vencimento
            _ meioDePagamento "(A Vista,credito, PIX)"
            _ tipoDeDocumento
            _ gerarBoletoeEmitirNotaFiscal 
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
            integer     nCodServico PK
            integer     nCodIntServico  "Codigo Integracao do Servico"
            text        cDescServ       "descricao do servico"
            string[9]   cNbs            "Codigo NBS do Servico"
            string[2]   cTribServ       "Tipo de Tributacao do Servico"
            decimal     nValUnit        "valor unitario do servico"
        }
        
    
  
```
