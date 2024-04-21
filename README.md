<!DOCTYPE html>
<html lang="ru">
<head>
   
<meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Депозитный калькулятор</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .calculator {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
            width: 300px;
            text-align: center;
        }

        h1 {
            color: #333;
        }

        form {
            margin-top: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #555;
        }

        input, select {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
        }

        button {
            background-color: #4caf50;
            color: #fff;
            padding: 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            width: 100%;
        }

        button:hover {
            background-color: #45a049;
        }

        #result {
            margin-top: 20px;
            font-weight: bold;
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Депозитный калькулятор</h1>
    <div class="calculator">
        <form id="depositForm">
            <label for="initialDeposit">Начальный депозит:</label>
            <input type="number" id="initialDeposit" name="initialDeposit" required><br>
            
            <label for="regularDeposit">Регулярное пополнение:</label>
            <input type="number" id="regularDeposit" name="regularDeposit"><br>

            <label for="depositFrequency">Период пополнения и капитализации:</label>
            <select id="depositFrequency" name="depositFrequency">
                <option value="monthly">Ежемесячно</option>
                <option value="quarterly">Ежеквартально</option>
                <option value="semi-annually">Дважды в год</option>
                <option value="annually">Ежегодно</option>
            </select><br>

            <label for="annualInterestRate"> Процентная ставка (%):</label>
            <input type="number" id="annualInterestRate" name="annualInterestRate" required><br>
            
            <label for="period">Срок вклада:</label>
            <select id="periodType" name="periodType">
                <option value="years">Годы</option>
                <option value="months">Месяцы</option>
            </select><br>

            <label for="periodDuration">Продолжительность срока:</label>
            <input type="number" id="periodDuration" name="periodDuration" required><br>

            <label for="capitalization">Капитализация:</label>
            <select id="capitalization" name="capitalization">
                <option value="simple">C капитализацией</option>
               <!-- <option value="compound">С капитализацией</option>-->
            </select><br>
            
           <!-- <label for="capitalizationPeriod">Период капитализации (если выбрана капитализация):</label>
            <label for="capitalizationPeriod">Период капитализации (если выбрана капитализация):</label>--> Место для записи


            <input type="number" id="capitalizationPeriod" name="capitalizationPeriod"><br> 


            
            <button type="submit">Рассчитать</button>
        </form>

        <div id="result"></div>
    </div>

    <script>
        document.getElementById('depositForm').addEventListener('submit', function(event) {
            event.preventDefault();
            var initialDeposit = parseFloat(document.getElementById('initialDeposit').value);
            var regularDeposit = parseFloat(document.getElementById('regularDeposit').value) || 0;
            var depositFrequency = document.getElementById('depositFrequency').value;
            var annualInterestRate = parseFloat(document.getElementById('annualInterestRate').value);
            var periodType = document.getElementById('periodType').value;
            var periodDuration = parseFloat(document.getElementById('periodDuration').value);
            var capitalization = document.getElementById('capitalization').value;
            var capitalizationPeriod = parseFloat(document.getElementById('capitalizationPeriod').value) || 0;
            
            var finalAmount = calculateDeposit(initialDeposit, regularDeposit, depositFrequency, annualInterestRate, periodType, periodDuration, capitalization, capitalizationPeriod);
            
            document.getElementById('result').innerHTML = "Конечная сумма депозита через указанный период составит: " + finalAmount.toFixed(2);
        });
        
        function calculateDeposit(initialDeposit, regularDeposit, depositFrequency, annualInterestRate, periodType, periodDuration, capitalization, capitalizationPeriod) {
            var interestRate = annualInterestRate / 100;
            var periodsPerYear = getPeriodsPerYear(periodType, depositFrequency);
            var totalPeriods = periodsPerYear * periodDuration;
            var finalAmount = initialDeposit;
            
            for (var i = 0; i < totalPeriods; i++) {
                if (capitalization === 'compound' && i % periodsPerYear === 0) {
                    finalAmount += regularDeposit;
                    finalAmount *= (1 + interestRate / periodsPerYear);
                } else if (capitalization !== 'compound') {
                    finalAmount += regularDeposit;
                    finalAmount *= (1 + interestRate / periodsPerYear);
                }
            }
            
            return finalAmount;
        }
        
        function getPeriodsPerYear(periodType, depositFrequency) {
            if (periodType === 'years') {
                if (depositFrequency === 'monthly') {
                    return 12;
                } else if (depositFrequency === 'quarterly') {
                    return 4;
                } else if (depositFrequency === 'semi-annually') {
                    return 2;
                } else if (depositFrequency === 'annually') {
                    return 1;
                }
            } else if (periodType === 'months') {
                return 1;
            }
        }
function depositCalculator() {
    var initialDeposit = parseFloat(document.getElementById('initialDeposit').value);
    var regularDeposit = parseFloat(document.getElementById('regularDeposit').value);
    var depositFrequency = parseFloat(document.getElementById('depositFrequency').value);
    var annualInterestRate = parseFloat(document.getElementById('annualInterestRate').value);
    var periodType = document.getElementById('periodType').value;
    var periodDuration = parseFloat(document.getElementById('periodDuration').value);
    var capitalization = document.getElementById('capitalization').value;
    var capitalizationPeriod = parseFloat(document.getElementById('capitalizationPeriod').value);

    var finalAmount = calculateDeposit(initialDeposit, regularDeposit, depositFrequency, annualInterestRate, periodType, periodDuration, capitalization, capitalizationPeriod);

    document.getElementById('finalAmount').innerHTML = finalAmount.toFixed(2);
}
    </script>

</body>
</html>
