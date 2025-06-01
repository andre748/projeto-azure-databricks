# projeto-azure-databricks
Azure Databricks para versionamento e organização de notebooks em ambientes de dados

# Projeto Azure Databricks

## 📌 Objetivos
- Provisionar um **Workspace Azure Databricks** no portal Azure.  
- Criar um **cluster Spark de nó único** para economizar recursos.  
- Importar o arquivo `products.csv` para uma **tabela Hive** dentro do Databricks.  
- Executar **consultas SQL** para exibir todos os registros da tabela.  
- Gerar um **gráfico de barras** que agrupa produtos por categoria.  
- Utilizar **DataFrame PySpark** para filtrar e exibir apenas os itens da categoria “Road Bikes”.

---

## 🛠️ Processos
1. **Criação do Workspace**  
   - No portal Azure, criar recurso “Azure Databricks”, definindo assinatura, grupo de recursos e nome.  
   - Selecionar tipo de preço (Premium ou Trial) e configurar o grupo de recursos gerenciados.  

2. **Provisionamento do Cluster**  
   - No Databricks, navegar até “Clusters” e clicar em “Create Cluster”.  
   - Escolher modo **Single Node**, Runtime **13.3 LTS ou superior**, node type `Standard_D4ds_v5`.  
   - Configurar para **terminar após 20 minutos** de inatividade e aguardar status “Running”.  

3. **Upload do CSV e Criação de Tabela Hive**  
   - Em “Data → Add Data”, selecionar “Create or modify table” e carregar `products.csv`.  
   - Definir nome da tabela como `products` (Hive Metastore, default schema).  

4. **Consulta SQL e Visualização**  
   - Criar um notebook SQL anexado ao cluster.  
   - Executar:
     ```
     import pandas as pd

      url = 'https://raw.githubusercontent.com/MicrosoftLearning/mslearn-databricks/main/data/products.csv'
      df = pd.read_csv(url)
      display(df)
     ```
   - Adicionar visualização “Bar”, definindo X = `Category` e Y = contagem de `ProductID`.  

5. **Análise com DataFrame PySpark**  
   - No mesmo notebook, adicionar célula Python e executar:
     ```python
     df = spark.sql("SELECT * FROM default.products")
     df_filtrado = df.filter(df.Category == 'Road Bikes')
     display(df_filtrado)
     ```
   - Exibir o DataFrame filtrado mostrando somente produtos de “Road Bikes”.  

---

## 🤖 Insights
- **Provisionamento Ágil**: Criação rápida do Workspace e do cluster no Azure Databricks.  
- **Eficiência de Recursos**: O modo Single Node foi suficiente para o exercício, consumindo menos vCPUs.  
- **Integração com Hive Metastore**: Importação de CSV tornou a criação de tabela e consultas SQL imediatas.    
- **Visualizações Prontas**: Gerar gráfico de barras diretamente no notebook facilita a exploração rápida dos dados.  
- **Boas Práticas**:  
 
