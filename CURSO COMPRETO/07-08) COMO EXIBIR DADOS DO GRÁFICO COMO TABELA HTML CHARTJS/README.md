# COMO EXIBIR DADOS DO GRÁFICO COMO TABELA HTML CHARTJS
Exibir os dados de um gráfico Chart.js em uma tabela HTML pode ser útil para fornecer uma visualização mais detalhada dos dados para os usuários. Aqui está como você pode fazer isso:

## Conceito:
O conceito envolve extrair os dados do gráfico Chart.js e inseri-los em uma tabela HTML. Isso pode ser feito acessando os datasets do gráfico e iterando sobre os valores para criar linhas e colunas na tabela.

## Exemplo de Implementação:
Aqui está um exemplo simples de como extrair dados de um gráfico de barras e exibi-los em uma tabela HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Exibição de Dados do Gráfico em Tabela HTML</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #dddddd;
      text-align: left;
      padding: 8px;
    }
    th {
      background-color: #4CAF50;
      color: white;
    }
    tr:nth-child(even) {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>
  <div class="container">
    <canvas id="barChart" width="800" height="400"></canvas>
    <table id="dataTable">
      <thead>
        <tr>
          <th>Label</th>
          <th>Value</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
    </table>
  </div>

  <script>
    const ctxBar = document.getElementById('barChart').getContext('2d');
    const barData = [12, 19, 3, 5, 2, 3];
    const labels = ['A', 'B', 'C', 'D', 'E', 'F'];

    new Chart(ctxBar, {
      type: 'bar',
      data: {
        labels: labels,
        datasets: [{
          label: 'Data',
          data: barData,
          backgroundColor: 'rgba(75, 192, 192, 0.2)',
          borderColor: 'rgba(75, 192, 192, 1)',
          borderWidth: 1
        }]
      },
      options: {
        plugins: {
          legend: {
            display: false
          }
        }
      }
    });

    const tableBody = document.querySelector('#dataTable tbody');
    labels.forEach((label, index) => {
      const row = tableBody.insertRow();
      const cell1 = row.insertCell(0);
      const cell2 = row.insertCell(1);
      cell1.textContent = label;
      cell2.textContent = barData[index];
    });
  </script>
</body>
</html>
```

## Explicação do Código:
1. **Configuração do Gráfico**:
   - Um gráfico de barras simples é criado usando Chart.js.

2. **Exibição dos Dados em uma Tabela**:
   - Uma tabela HTML é definida com cabeçalhos para "Label" e "Value".
   - Os dados do gráfico (rótulos e valores) são iterados.
   - Para cada rótulo, uma nova linha é inserida na tabela.
   - Cada linha recebe o rótulo e o valor correspondente como células.

Ao atualizar o gráfico, os dados da tabela também serão atualizados automaticamente. Isso fornece uma maneira eficiente de exibir os dados do gráfico em um formato tabular para análise mais detalhada.