<script>
import {monthNames, weekDayNames} from '../config/config.js';

export default {
	name: 'cal-month',
	props: {
		month: {
				type: Number,
				default: 0
		},
		year: {
				type: Number,
				default: 0
		}
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
		let startDate = new Date(this.year, this.month, 1); // primeiro dia do mês
		let curYear = startDate.getFullYear();
		let dayInWeek = startDate.getDay();
		let curMonth = startDate.getMonth();

		// Gerar linha de header com os nomes dos dias da semana
		for (var weekDay of weekDayNames) {
			children.push(createElement('span', {'class': 'day'}, ' ' + weekDay + ' '));
		}

		// Padding até ao dia da semana correspondente ao início do mês actual
		let monthStartsAtDayOfWeek =  startDate.getDay();

		for (var k=1; k<monthStartsAtDayOfWeek; k++) {
			children.push(createElement('span', {'class': 'day'}, ''));
		}

		let endOfMonth = new Date(curYear, curMonth + 1, 0);
		let day = new Date(curYear, curMonth, 1);

		while(day.getDate() < endOfMonth.getDate()) {
			// Gerar span com o dia actual
			children.push(createElement('a', {
				'domProps': {
				'date': day.toLocaleDateString(),
				'teste': 123
				},
				'attrs': {
						href: '#'
				},
				'class': 'day',
				'on': {
						'click': this.testaclick
					}
				}, 
				day.getDate()));

				day.setDate(day.getDate() + 1);
		}

		// Padding para fazer o próximo mês começar na linha seguinte
		for (let k = endOfMonth.getDay(); k < 7;  k++) {
			children.push(createElement('span', {'class': 'day'}, ' '));
		}

		return createElement('div',   // tag name
			{class: 'month'},
			children // array of children
		);
	}
}
</script>

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
.month {
  display: flex;
  width: 350px;
  justify-content:flex-start;
  flex-direction: row;
  flex-wrap:wrap;
  border:1px solid blue;
	align-content: space-between;
	flex-grow: 1;
	padding: 20px;
}

.day {
  width: calc(100% / 7);
  box-sizing: border-box;
  height: 25px;
  line-height: 24px;
  align-content: stretch;
  text-align: right;
}

.day.grow {
  width: 100%;
  flex-grow: 7;
  text-align: center;
}

.day.past {
  color: red;
}

</style>
