const N = +readline();
// Benford's law constants significant digits
const BENFORD = [301, 176, 125, 97, 79, 67, 58, 51, 46];
// make an array of only first digits 
let data = Array(N).fill().map(v => [...readline()].find(d => !isNaN(+d) && d > 0));
// transform it into an array of frequencies in per ten
let prob = data.reduce((acc, cur) => (acc[cur - 1] += 1) && acc, Array(9).fill(0))
                .map(v => (v / N) * 1000);
// use benford constants to detect anomaly, if any
let res = prob.findIndex((v, i) => v < Math.max(BENFORD[i] - 100, 0) || v > BENFORD[i] + 100) > -1;
console.log(res);
