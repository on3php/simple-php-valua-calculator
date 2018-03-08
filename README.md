# simple-php-valua-calculator
Very simple valuta calculator in php using Google finance

This is my second project i make public so if there are things i don't do well please let me know.
I made this very basic valuta calculator in php using Google Finance to get a indication of the exchange rate

I'm not the best programmer, all i know came from selfstudy and many hours of trial and error procedure -;)

So here it is

You can change or add more currency's if you wish, but that is all that i needed and so it is a base for building your project on

<?

if (isset($_POST['action'])){
	$fromAmount = $_POST['fromAmount'];
	$fromCurrency = $_POST['fromCurrency'];
	$toCurrency = $_POST['toCurrency'];
	
	$link_api = 'https://finance.google.com/finance/converter?a='.$fromAmount.'&from='.$fromCurrency.'&to='.$toCurrency;
	$data = file_get_contents($link_api);
	preg_match("/<span class=bld>(.*)<\/span>/",$data, $converted);
	$toAmount = $converted[1];
}else{
	$fromAmount = '1';	
}
// exchange indication
$link_api = 'https://finance.google.com/finance/converter?a=1&from=GBP&to=EUR';
$data = file_get_contents($link_api);
preg_match("/<span class=bld>(.*)<\/span>/",$data, $converted);
$GBPtoEuroAmount = $converted[1];
$link_api = 'https://finance.google.com/finance/converter?a=1&from=EUR&to=GBP';
$data = file_get_contents($link_api);
preg_match("/<span class=bld>(.*)<\/span>/",$data, $converted);
$EurotoGBPAmount = $converted[1];
?>

<style>
.frm {
	border-color: blue;
}
.lgdfrm {
	color: blue;
	padding: 5px;	
}

.to {
	border-color: lightblue;
}

.lgdto {
	color: lightblue;
	padding: 5px;	
}
</style>


<fieldset>
	<legend>Valuta calulator</legend>
	<form method="post" action="">
		<fieldset class="frm">
			<legend class="lgdfrm">From</legend>
			<input name="fromAmount" type="text" size="15" value="<? echo $fromAmount; ?>">
			<select name="fromCurrency">
				<?
				if ($fromCurrency == 'GBP' || $fromCurrency == '') {
					echo '
					<option selected value="GBP">Britsh pounds</option>
					<option value="EUR">Euro</option>
					';
				}
				if ($fromCurrency == 'EUR') {
					echo'
					<option value="GBP">Britsh pounds</option>
					<option selected value="EUR">Euro</option>
					';
				}
				?>						
			</select>
			<p>
		</fieldset>
		<p>
		<fieldset class="to">
			<legend class="lgdto">To</legend>
			Amount: <? echo '<b>'.$toAmount.'</b>'; ?>
			<select name="toCurrency">
				<?
				if ($toCurrency == 'GBP') {
					echo '
					<option selected value="GBP">Britsh pounds</option>
					<option value="EUR">Euro</option>
					';
				}
				if ($toCurrency == 'EUR'|| $toCurrency == '') {
					echo'
					<option value="GBP">Britsh pounds</option>
					<option selected value="EUR">Euro</option>
					';
				}
				?>										
			</select>
			<p>
		</fieldset>
		<hr>
		<button type="submit" name="action" value="action">Calulate</button>
		<p align="center">(1 GBP = <? echo $GBPtoEuroAmount; ?> / 1 EUR = <? echo $EurotoGBPAmount ?>)</p>
	</form>
</fieldset>
