<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
    <title>Stock Price Prediction Demo</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background: #10141e;
            color: #e0e0e0;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            box-sizing: border-box;
        }
        h1 {
            color: #61dafb;
            margin-bottom: 10px;
            font-weight: 700;
        }
        .chart-container {
            width: 100%;
            max-width: 400px;
            margin: 10px auto 40px auto;
        }
        canvas {
            border-radius: 8px;
            background: #1e2430;
            box-shadow: 0 0 12px #0a84ff44;
            width: 100% !important;
            height: auto !important;
        }
        .prediction, .metrics {
            background: #1e2430;
            border-radius: 12px;
            padding: 15px 20px;
            width: 100%;
            max-width: 400px;
            margin: 10px 0;
            box-shadow: 0 0 15px #61dafb55;
        }
        .label {
            font-weight: 600;
            color: #a0c4ff;
        }
        @media (max-width: 400px) {
            body {
                padding: 10px;
            }
            .chart-container, .prediction, .metrics {
                max-width: 100%;
            }
        }
    </style>
</head>
<body>
    <h1>Stock Price Prediction Demo</h1>

    <div class="prediction">
        <div><span class="label">LSTM Next Day Prediction:</span> ₹1503.72</div>
    </div>

    <div class="metrics">
        <div><span class="label">Model Evaluation - RMSE:</span> 12.45</div>
        <div><span class="label">Model Evaluation - MAE:</span> 9.98</div>
    </div>

    <div class="chart-container">
        <canvas id="priceChart" aria-label="Stock prices and forecast chart" role="img"></canvas>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.3.0/dist/chart.umd.min.js"></script>
    <script>


        const dates = [
            "2024-04-01","2024-04-02","2024-04-03","2024-04-04","2024-04-05",
            "2024-04-06","2024-04-07","2024-04-08","2024-04-09","2024-04-10",
            "2024-04-11","2024-04-12","2024-04-13","2024-04-14","2024-04-15",
            "2024-04-16","2024-04-17","2024-04-18","2024-04-19","2024-04-20",
            "2024-04-21","2024-04-22","2024-04-23","2024-04-24","2024-04-25",
            "2024-04-26","2024-04-27","2024-04-28","2024-04-29","2024-04-30"
        ];

        const actualPrices = [
            1480,1478,1476,1485,1492,1498,1500,1503,1506,1508,
            1510,1507,1505,1502,1500,1507,1512,1518,1520,1523,
            1520,1515,1510,1505,1507,1510,1513,1515,1518,1520
        ];

        const forecastDates = [
            "2024-05-01","2024-05-02","2024-05-03","2024-05-04","2024-05-05"
        ];
        const forecastPrices = [1523, 1525, 1527, 1528, 1530];


        const combinedDates = [...dates, ...forecastDates];
        const combinedPrices = [...actualPrices, ...Array(forecastPrices.length).fill(null)];
        const forecastedData = Array(actualPrices.length).fill(null).concat(forecastPrices);


        const ctx = document.getElementById('priceChart').getContext('2d');
        const priceChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: combinedDates,
                datasets: [
                    {
                        label: 'Actual Close Price',
                        data: combinedPrices,
                        borderColor: '#61dafb',
                        backgroundColor: '#61dafb66',
                        tension: 0.3,
                        fill: false,
                        pointRadius: 3,
                        pointHoverRadius: 6,
                        borderWidth: 2,
                    },
                    {
                        label: 'Forecasted Price',
                        data: forecastedData,
                        borderColor: '#ff6f61',
                        backgroundColor: '#ff6f6133',
                        borderDash: [8, 6],
                        tension: 0.3,
                        fill: false,
                        pointRadius: 3,
                        pointHoverRadius: 6,
                        borderWidth: 2,
                    }
                ]
            },
            options: {
                responsive: true,
                interaction: {
                    mode: 'nearest',
                    axis: 'x',
                    intersect: false,
                },
                plugins: {
                    legend: {
                        labels: {
                            color: '#e0e0e0',
                            font: { size: 14 }
                        }
                    },
                    tooltip: {
                        mode: 'index',
                        intersect: false,
                    },
                    title: {
                        display: true,
                        text: 'Stock Closing Prices and Forecast',
                        color: '#61dafb',
                        font: { size: 18, weight: 'bold' },
                        padding: { top: 10, bottom: 20 },
                    },
                },
                scales: {
                    x: {
                        ticks: { color: '#a0a0a0' },
                        grid: { color: '#2a2f3a' }
                    },
                    y: {
                        ticks: { color: '#a0a0a0' },
                        grid: { color: '#2a2f3a' },
                        beginAtZero: false
                    }
                }
            }
        });
    </script>
</body>
</html>
</content>
</create_file>

<attempt_completion>


