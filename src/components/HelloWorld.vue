<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    testaclick(evt) {
      evt.preventDefault();
      let date = evt.target.date;

      console.log(date);
    }
  },
  render: function(createElement) {
    let children = [];
    let today = new Date();
    console.log(today);

    let monthNames = [
      'JAN',
      'FEV',
      'MAR',
      'ABR',
      'MAI',
      'JUN',
      'JUL',
      'AGO',
      'SET',
      'OUT',
      'NOV',
      'DEZ'
    ];

    let weekDayNames = ['SEG', 'TER', 'QUA', 'QUI', 'SEX', 'SAB', 'DOM'];
    
    let curDate = today.getDate();
    let curYear = today.getFullYear();
    let dayInWeek = today.getDay();
    let curMonth = today.getMonth();

    // Gerar linha de header com os nomes dos dias da semana
    for (var day of weekDayNames) {
      children.push(createElement('span', {'class': 'day'}, ' ' + day + ' '));
    }

    // Padding até ao dia da semana correspondente ao início do mês actual
    let monthStartsAtDayOfWeek =  new Date(curYear, curMonth, 1).getDay();
    for (var k=1; k<monthStartsAtDayOfWeek; k++) {
      children.push(createElement('span', {'class': 'day'}, ''));
    }

    // Gerar os dias no passado até ao início do mês
    for (var j=1; j<curDate; j++) {
      let pastDay = new Date(curYear, curMonth, j);
      children.push(createElement('span', {'class': 'day past'}, pastDay.getDate()));
    }

    // Gerar calendário para até um ano no futuro
    for (var i=0; i<365; i++) {
      let curYear = today.getFullYear();
      let curDate = today.getDate();
      let curMonth = today.getMonth();
      let curDayOfWeek = today.getDay();

      // Calcular o número de dias existentes neste mês
      let daysInMonth = new Date(2018, curMonth + 1, 0).getDate();

      // Gerar span com o dia actual
      children.push(createElement('a', {
        'domProps': {
          'date': today.toLocaleDateString(), 
          'teste': 123
          },
          'attrs': {
            href: '#'
          },
          'class': 'day', 
          'on': {
            'click': this.testaclick
          }
        }, today.getDate()));

      // Se chegámos ao fim do mês
      if (curDate == daysInMonth) {
        // Padding para fazer o próximo mês começar na linha seguinte
        for (var k = curDayOfWeek; k < 7;  k++) {
          children.push(createElement('span', {'class': 'day'}, ' '));
        }

        // Inserir o nome do mês + ano
        let nextMonth = new Date(curYear, curMonth, daysInMonth + 1).getMonth();
        let nextMonthYear = new Date(curYear, curMonth, daysInMonth + 1).getFullYear();
        children.push(createElement('span', {'class': 'day grow'}, monthNames[nextMonth] + ' ' + nextMonthYear));

        // Inserir mais um linha de header com os nomes dos dias da semana
        for (var day of weekDayNames) {
          children.push(createElement('span', {'class': 'day'}, ' ' + day + ' '));
        }

        // Padding até o dia do mês se iniciar no dia da semana correcto
        for (var k = 0; k < curDayOfWeek; k++) {
          children.push(createElement('span', {'class': 'day'}, ' '));
        }
      } 
      
      today.setDate(curDate + 1);
    }
    
    return createElement(
      'div',   // tag name
      {class: 'calendar'},
      children // array of children
    );
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.calendar {
  display: flex;
  width: 350px;
  justify-content:flex-start;
  flex-direction: row;
  flex-wrap:wrap;
  
  margin: auto;
}

.day.grow {
  width: 100%;
  flex-grow: 7;
  text-align: center;
}

.day.past {
  color: red;
}

.day {
  width: calc(350px / 7);
  box-sizing: border-box;
  height: 25px;
  line-height: 24px;
  align-content: stretch;
  text-align: right;
}

.day:nth-child(7n) {
   
}

.day:nth-last-child(-n+7) {
  
}

.day:last-child {
  
}
</style>
