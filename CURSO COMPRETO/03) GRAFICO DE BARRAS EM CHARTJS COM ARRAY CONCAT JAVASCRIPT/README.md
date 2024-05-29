# GRAFICO DE BARRAS EM CHARTJS COM ARRAY CONCAT JAVASCRIPT
## Conceito: Concatenação de Arrays em JavaScript
A concatenação de arrays em JavaScript é o processo de combinar dois ou mais arrays em um único array. Isso é feito usando o método `concat()`.

## Sintaxe:
```javascript
const newArray = array1.concat(array2);
```

- `array1`, `array2`: Os arrays a serem concatenados.
- `newArray`: O novo array resultante da concatenação de `array1` e `array2`.

### Exemplo:
```javascript
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
const newArray = array1.concat(array2);
console.log(newArray); // Output: [1, 2, 3, 4, 5, 6]
```

Neste exemplo, `newArray` contém todos os elementos de `array1` seguidos pelos elementos de `array2`.

## Aplicação em Gráfico de Barras com Chart.js
Agora, vamos aplicar o conceito de concatenação de arrays para criar um gráfico de barras em Chart.js com dados de dois arrays diferentes.

### Exemplo:
Suponha que temos os seguintes dados de vendas para dois meses diferentes:

```javascript
const labels = ['January', 'February'];
const salesMonth1 = [100, 150];
const salesMonth2 = [120, 160];
```

Para criar um gráfico de barras com esses dados usando Chart.js, podemos concatenar os arrays `salesMonth1` e `salesMonth2` em um único array e usar os rótulos correspondentes de `labels`:

```javascript
const allSalesData = salesMonth1.concat(salesMonth2);

const ctx = document.getElementById('barChart').getContext('2d');
const barChart = new Chart(ctx, {
  type: 'bar',
  data: {
    labels: labels.concat(labels),
    datasets: [{
      label: 'Sales',
      data: allSalesData,
      backgroundColor: 'rgba(255, 99, 132, 0.2)',
      borderColor: 'rgba(255, 99, 132, 1)',
      borderWidth: 1
    }]
  },
  options: {
    scales: {
      y: {
        beginAtZero: true
      }
    }
  }
});
```

Neste exemplo, `allSalesData` contém os dados de vendas para ambos os meses concatenados em um único array. O gráfico de barras resultante mostrará as vendas para os dois meses distintos.