var distributor = "sephora";
var codigoEmbed = "9sOHolOi22I,";

//Verifica se tem nossa div automática e cria/adiciona se não tiver (GTM ou LP)
var divStdAuto = document.querySelectorAll('#standoutDivAutomatico');
if (divStdAuto.length <= 0) {
	var divStd = document.createElement("div");
	divStd.setAttribute("id", "standoutDivAutomatico");

	var divRefVarejo = document.querySelector("#pdpMain .product-info .tabs-content");
	if (divRefVarejo) {
        //Insere após a DIV de referência (mesmo nível)
        divRefVarejo.insertAdjacentElement('afterend', divStd);
	}

	// Verificação para inclusão da DIV Standout somente na página de Marca Sephora
	if (window.location.href.indexOf("/sephora-collection/?content=definition") >= 0) {
		var divRefVarejoPagMarca = document.querySelector(".bcr__wrapper .bcr__content");
		if (divRefVarejoPagMarca) {
			//Insere dentro da referência na última posição
			divRefVarejoPagMarca.appendChild(divStd);
		}
	}
}

/*	Executa JS quando a div é encontrada (carregamento)	*/
function waitForElm(selector) {
	return new Promise(resolve => {
		if (document.querySelector(selector)) {
			return resolve(document.querySelector(selector));
		}

		const observer = new MutationObserver(mutations => {
			if (document.querySelector(selector)) {
				resolve(document.querySelector(selector));
				observer.disconnect();
			}
		});

		observer.observe(document.body, {
			childList: true,
			subtree: true
		});
	});
}
waitForElm('#standoutDivAutomatico').then(elm => StandoutJSInit());
waitForElm('.product-price .price-box .price-sales span').then(elm => catchProductData());

function StandoutJSInit(){
		// console.log('StandoutJSInit');
		
		if(sessionStorage.getItem('StandoutSession') == 'true' && sessionStorage.getItem('StandoutUrl') == window.location.href){
			console.log('StandoutJSInit - Chamada duplicada');
			sessionStorage.setItem('StandoutSession', '');
			sessionStorage.setItem('StandoutUrl', '');
		} else {
			// console.log('StandoutJSInit - Chamada');
			sessionStorage.setItem('StandoutSession', 'true');
			sessionStorage.setItem('StandoutUrl', window.location.href);
			StandoutJS();
		}
}

function StandoutJS(){
	
	var bot=false;
	var botPattern = "(googlebot\/|Googlebot-Mobile|Googlebot-Image|Google favicon|Mediapartners-Google|bingbot|slurp|java|wget|curl|Commons-HttpClient|Python-urllib|libwww|httpunit|nutch|phpcrawl|msnbot|jyxobot|FAST-WebCrawler|FAST Enterprise Crawler|biglotron|teoma|convera|seekbot|gigablast|exabot|ngbot|ia_archiver|GingerCrawler|webmon |httrack|webcrawler|grub.org|UsineNouvelleCrawler|antibot|netresearchserver|speedy|fluffy|bibnum.bnf|findlink|msrbot|panscient|yacybot|AISearchBot|IOI|ips-agent|tagoobot|MJ12bot|dotbot|woriobot|yanga|buzzbot|mlbot|yandexbot|purebot|Linguee Bot|Voyager|CyberPatrol|voilabot|baiduspider|citeseerxbot|spbot|twengabot|postrank|turnitinbot|scribdbot|page2rss|sitebot|linkdex|Adidxbot|blekkobot|ezooms|dotbot|Mail.RU_Bot|discobot|heritrix|findthatfile|europarchive.org|NerdByNature.Bot|sistrix crawler|ahrefsbot|Aboundex|domaincrawler|wbsearchbot|summify|ccbot|edisterbot|seznambot|ec2linkfinder|gslfbot|aihitbot|intelium_bot|facebookexternalhit|yeti|RetrevoPageAnalyzer|lb-spider|sogou|lssbot|careerbot|wotbox|wocbot|ichiro|DuckDuckBot|lssrocketcrawler|drupact|webcompanycrawler|acoonbot|openindexspider|gnam gnam spider|web-archive-net.com.bot|backlinkcrawler|coccoc|integromedb|content crawler spider|toplistbot|seokicks-robot|it2media-domain-crawler|ip-web-crawler.com|siteexplorer.info|elisabot|proximic|changedetection|blexbot|arabot|WeSEE:Search|niki-bot|CrystalSemanticsBot|rogerbot|360Spider|psbot|InterfaxScanBot|Lipperhey SEO Service|CC Metadata Scaper|g00g1e.net|GrapeshotCrawler|urlappendbot|brainobot|fr-crawler|binlar|SimpleCrawler|Livelapbot|Twitterbot|cXensebot|smtbot|bnf.fr_bot|A6-Indexer|ADmantX|Facebot|Twitterbot|OrangeBot|memorybot|AdvBot|MegaIndex|SemanticScholarBot|ltx71|nerdybot|xovibot|BUbiNG|Qwantify|archive.org_bot|Applebot|TweetmemeBot|crawler4j|findxbot|SemrushBot|yoozBot|lipperhey|y!j-asr|Domain Re-Animator Bot|AddThis)";
	var re = new RegExp(botPattern, 'i');
	var userAgent = navigator.userAgent;
	if (re.test(userAgent)) {
	  bot=true;
	}

	var nVer = navigator.appVersion;
	var nAgt = navigator.userAgent;
	var browserName  = navigator.appName;
	var fullVersion  = ''+parseFloat(navigator.appVersion); 
	var majorVersion = parseInt(navigator.appVersion,10);
	var nameOffset,verOffset,ix;

	if ((verOffset=nAgt.indexOf('OPR/'))!=-1) {
	 browserName = 'Opera';
	 fullVersion = nAgt.substring(verOffset+4);
	}
   
	else if ((verOffset=nAgt.indexOf('Opera'))!=-1) {
	 browserName = 'Opera';
	 fullVersion = nAgt.substring(verOffset+6);
	 if ((verOffset=nAgt.indexOf('Version'))!=-1) 
	   fullVersion = nAgt.substring(verOffset+8);
	}
   
	else if ((verOffset=nAgt.indexOf('MSIE'))!=-1) {
	 browserName = 'Microsoft Internet Explorer';
	 fullVersion = nAgt.substring(verOffset+5);
	}
   
	else if ((verOffset=nAgt.indexOf('Chrome'))!=-1) {
	 browserName = 'Chrome';
	 fullVersion = nAgt.substring(verOffset+7);
	}
   
	else if ((verOffset=nAgt.indexOf('Safari'))!=-1) {
	 browserName = 'Safari';
	 fullVersion = nAgt.substring(verOffset+7);
	 if ((verOffset=nAgt.indexOf('Version'))!=-1) 
	   fullVersion = nAgt.substring(verOffset+8);
	}
   
	else if ((verOffset=nAgt.indexOf('Firefox'))!=-1) {
	 browserName = 'Firefox';
	 fullVersion = nAgt.substring(verOffset+8);
	}
   
	else if ( (nameOffset=nAgt.lastIndexOf(' ')+1) < 
			  (verOffset=nAgt.lastIndexOf('/')) ) 
	{
	 browserName = nAgt.substring(nameOffset,verOffset);
	 fullVersion = nAgt.substring(verOffset+1);
	 if (browserName.toLowerCase()==browserName.toUpperCase()) {
	  browserName = navigator.appName;
	 }
	}
	
	if ((ix=fullVersion.indexOf(';'))!=-1)
	   fullVersion=fullVersion.substring(0,ix);
	if ((ix=fullVersion.indexOf(' '))!=-1)
	   fullVersion=fullVersion.substring(0,ix);

	majorVersion = parseInt(''+fullVersion,10);
	if (isNaN(majorVersion)) {
	 fullVersion  = ''+parseFloat(navigator.appVersion); 
	 majorVersion = parseInt(navigator.appVersion,10);
	}
	
	var url = window.location.href;
	var urlNew = url.replace("/#/", "/");
	
	// CATCH EAN /*************************
	var sku = getEan();
	// CATCH EAN /*************************

	// CATCH PRECO/disponibilidade /*************************
	var preco = getRegularPrice();
	var disponibilidade = getAvailability();
	try {
		

		
	} catch (e) {
		console.log('Não conseguiu pegar o preço', e );
	}
	// CATCH PRECO /*************************

	var action = 'PageView';
	var browserName = browserName;
	var browserVersion = fullVersion; 
	var geolocation = navigator.geolocarion; 
	var language = navigator.language; 
	var plataform = navigator.plataform;
	var retailerDomain = window.location.hostname;
	var monitored = 'false';

	var data = "distributor="+distributor+"&sku="+sku+"&url="+encodeURIComponent(urlNew)+"&action="+action+"&browserName="+browserName+"&browserVersion="+browserVersion+"&geolocation="+geolocation+"&language="+language+"&plataform="+plataform+"&monitored="+monitored+"&preco="+preco+"&disponibilidade="+disponibilidade+"&bot="+bot;
	var urlCatch = 'https://standout.com.br/'+distributor+'/catchtagSephora.php?'+data;
		
	setTimeout(function () {
		var xmlhttp = new XMLHttpRequest();
		xmlhttp.onreadystatechange = function () {
			if (this.readyState == 4 && this.status == 200) {
				var myObj = JSON.parse(this.responseText);
				console.log(myObj);

				// VERIFICA SE TEM MINI VITRINE
				if ((!myObj.mv == "" || !myObj.mv == null) && (myObj.mv.length > 0)) {


					var stdMVBTSContainer = document.getElementById("std-mv-bts-container");

					if (stdMVBTSContainer == null) {

						function getScript(url, callback) {
							var scriptMVStd = document.createElement('script');
							scriptMVStd.type = 'text/javascript';
							scriptMVStd.src = url;
							scriptMVStd.onload = callback;

							document.getElementsByTagName('head')[0].appendChild(scriptMVStd);
						}

						getScript("https://s3-sa-east-1.amazonaws.com/assets.standout.com.br/js/scripts-minivitrines.js", function () {

							//Adiciona CSS das MINI Vitrines
							stdAddCssMV("https://s3-sa-east-1.amazonaws.com/assets.standout.com.br/css/style-mv-assets.css");

							// Custom CSS Botões das MINI Vitrines
							var MVCustomstyles = ".btn-open-special-container{max-width: 160px; z-index: 10;} .btn-open-special-container.horizontal {width: 160px; margin: 36px 0 0 4px;} .btn-open-special-container.horizontal.mobile {margin: 78px 0 0 6px;} .btn-open-special-animated {width: 36px; height: 36px; border: 3px solid rgb(32, 32, 32, .8); background: #202020; animation: iconPulse 0.7s ease-out 0s infinite alternate running;} @keyframes iconPulse { 0% { box-shadow: 0 0 0px #202020; } 50% { box-shadow: 0 0 16px #202020;} 100% { box-shadow: 0 0 20px #202020;}} .btn-audio svg g path {animation: iconPulseInner 0.7s ease-out 0s infinite alternate running;} @keyframes iconPulseInner { 0% {fill: #ffffff;} 100% {fill: ##353535;}} .svg.std-icon-animated {max-width: 36px; max-height: 36px;}"
							var styleSheet = document.createElement("style");
							styleSheet.innerText = MVCustomstyles;
							document.head.appendChild(styleSheet);

							//Variável para guardar a referência de onde deve entrar "geralmente desktop"
							//Botões
							var refIDStdProd = document.querySelector('.product-image-container');
							//Mini Vitrines
							var refIDStdProdMV = document.querySelector('#wrapper');

							//Verifica se as referências Desktop existem, pois elas podem mudar quando estão na versão mobile
							if (refIDStdProd == null) {
								//Se vazia, faz tratamentos para versão mobile, buscando nova referência e setando "MVCustomMobile" true
								var refIDStdProd = document.querySelector('.product-image-container');
								var MVCustomMobile = true;
							}
							if (refIDStdProdMV == null) {
								var refIDStdProdMV = document.querySelector('#wrapper');
							}

							//Criando a DIV de marcação da Standout com ID para inserir os botões das mini vitrines
							var divSTDProductID = document.createElement('div');
							divSTDProductID.id = "productStdID";
							divSTDProductID.setAttribute("style", "position: relative;");

							//Criando a DIV de marcação da Standout com ID para inserir os conteúdos das mini vitrines
							var divSTDProductIDMV = document.createElement('div');
							divSTDProductIDMV.id = "productStdIDMV";

							//Insere conteúdos na DIV da Standout antes da DIV de referência
							function insertBefore(el, referenceNode) {
								referenceNode.parentNode.insertBefore(el, referenceNode);
							}
							insertBefore(divSTDProductID, refIDStdProd);
							insertBefore(divSTDProductIDMV, refIDStdProdMV);

							//Adicionando o container dos botões das MINI Vitrines (Desktop ou Mobile)
							if (!MVCustomMobile) {
								var MVBTS = "<div id='std-mv-bts-container' class='btn-open-special-container horizontal'></div>";
							} else {
								var MVBTS = "<div id='std-mv-bts-container' class='btn-open-special-container horizontal mobile'></div>";
							}
							document.getElementById("productStdID").innerHTML += MVBTS;

							//Adicionando os botões das MINI Vitrines
							setTimeout(function () {
								for (var i = 0; i < myObj.mv.length; i++) {

									var stdMVSlug = myObj.mv[i].slug;

									//Verifica e adiciona so botões
									if (myObj.mv[i].tipo == "mv-foto") {
										var MVBtFoto = "<div class='btn-open-special-animated horizontal' id='btn-" + stdMVSlug + "'><a href='#" + stdMVSlug + "' onclick='hitstdmv(\"" + myObj.mv[i].industria + "\",\"" + codigoEmbed + "\",\"" + myObj.mv[i].slugCat + "\",\"" + stdMVSlug + "\");'><svg class='std-icon-animated' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='#FFFFFF' stroke-width='3' stroke-linecap='round' stroke-linejoin='round'><title>Clique para ver mais informações</title><line x1='12' y1='5' x2='12' y2='19'></line><line x1='5' y1='12' x2='19' y2='12'></line></svg></a></div>";
										document.getElementById("std-mv-bts-container").innerHTML += MVBtFoto;
									} else if (myObj.mv[i].tipo == "mv-video") {
										var MVBtVideo = "<div class='btn-open-special-animated horizontal' id='btn-" + stdMVSlug + "'><a href='#" + stdMVSlug + "' onclick='hitstdmv(\"" + myObj.mv[i].industria + "\",\"" + codigoEmbed + "\",\"" + myObj.mv[i].slugCat + "\",\"" + stdMVSlug + "\");'><svg class='std-icon-animated' viewBox='0 0 48 48' xmlns='http://www.w3.org/2000/svg'><path d='M16 10v28l22-14z' fill='#FFFFFF' stroke='#FFFFFF' stroke-width='3' stroke-linecap='round' stroke-linejoin='round'/></svg></a></div>";
										document.getElementById("std-mv-bts-container").innerHTML += MVBtVideo;
									} else if (myObj.mv[i].tipo == "mv-audio"){
										var MVBtAudio = "<div class='btn-open-special-animated horizontal btn-audio' id='btn-"+stdMVSlug+"'><a href='#"+stdMVSlug+"' onclick='hitstdmv(\""+myObj.mv[i].industria+"\",\""+codigoEmbed+"\",\""+myObj.mv[i].slugCat+"\",\""+stdMVSlug+"\"); playStdMVAudio();'><svg class='std-icon-animated' viewBox='0 0 26 26' xmlns='http://www.w3.org/2000/svg' width='46' height='46' ><title>Clique para ouvir a descrição</title><g transform='translate(0 -1028.362)'><path fill='#fff' style='line-height:normal;text-indent:0;text-align:start;text-decoration-line:none;text-transform:none;block-progression:tb' d='M 8,0 C 6.3466486,0 5,1.3467 5,3 l 0,5 c 0,1.6534 1.3466486,3 3,3 1.6533514,0 3,-1.3466 3,-3 L 11,3 C 11,1.3467 9.6533514,0 8,0 Z M 3,8.1523438 c 0,2.5124892 1.9849527,4.5377522 4.5,4.7832032 l 0,2.048828 0,0.01563 -2,0 0,1 5,0 0,-1 -2,0 0,-0.01563 0,-2.048828 C 11.015048,12.690096 13,10.664833 13,8.1523438 l -1,0 c 0,2.1220002 -1.765404,3.8320312 -4,3.8320312 -2.2345965,0 -4,-1.710031 -4,-3.8320312 z' transform='translate(3.5 1031.362)'/></g></svg></a></div>";
										document.getElementById("std-mv-bts-container").innerHTML+=MVBtAudio;
									}

									//Adiciona os conteúdos das DIVs
									document.getElementById("productStdIDMV").innerHTML += myObj.mv[i].div;

									//Imprime o conteúdo das MINI Vitrines
									writeStandoutMV(myObj.mv[i].tipo);

									//Remove botões e DIVs duplicadas se houver
									var divMVProductRemove = document.querySelectorAll('#productStdID');
									if (divMVProductRemove.length > 1) { divMVProductRemove[1].remove(); }

									var btnMVRemove = document.querySelectorAll('#btn-' + stdMVSlug);
									if (btnMVRemove.length > 1) { btnMVRemove[1].remove(); }

									var divMVRemove = document.querySelectorAll('#' + stdMVSlug);
									if (divMVRemove.length > 1) { divMVRemove[1].remove(); }

									var containerMVRemove = document.querySelectorAll('#std-mv-bts-container');
									if (containerMVRemove.length > 1) { containerMVRemove[1].remove(); }

									console.log(stdMVSlug);
								}
							}, '1000');
						});
					}
				}

				var divStandoutAutomatico = document.getElementById("standoutDivAutomatico");
				if (divStandoutAutomatico) {
					divStandoutAutomatico.innerHTML = myObj.div.replace(/<br>/g, "");
					writeStandoutCBP();
				}
			}
		};
		xmlhttp.open("GET", urlCatch, true);
		xmlhttp.send();

	}, 1000);

	function writeStandoutMV(tipo) {
		var elem = document.getElementById("standoutDivMV-" + tipo);
		var w = parseInt(window.innerWidth);
		var h = parseInt(elem.getAttribute("h"));
		var hmv = parseInt(h - (h * 0.14));
		//console.log('w/h/hmv:', w, h, hmv);

		if ( w > 768) { w = "768"; }
		else if ((w <= 768) && (w > 475)) { w = w-40; }
		else if ((w <= 475) && (w > 320)) { w = w-40; h = hmv; }
		else { w = w-40; }

		var p = ((elem.getAttribute("p") === null) ? codigoEmbed : elem.getAttribute("p")) + '/' + elem.getAttribute("x") + '/' + elem.getAttribute("y");
		var c = elem.getAttribute("i");
		elem.style.height = h + 'px';
		elem.innerHTML = '<iframe referrerpolicy="no-referrer-when-downgrade" width="' + w + '" height="' + parseInt(h) + '" src="//www.standout.com.br/' + c + '/p/' + p + '" frameborder="0" scrolling="no" id="frameStandoutMV' + tipo + '" allow="autoplay" allowfullscreen></iframe>';
	}
	
	function writeStandoutCBP() {
		if (document.getElementById("standoutDiv") != null) {
			if (document.getElementById("standoutDiv").getAttribute("h") != null || document.getElementById("standoutDiv").getAttribute("h") != "undefined") {
				var elem = document.getElementById("standoutDiv");
				var w = '100%';
				var h = parseInt(elem.getAttribute("h"));
				var p = ((elem.getAttribute("p") === null) ? codigoEmbed : elem.getAttribute("p")) + '/' + elem.getAttribute("x") + '/' + elem.getAttribute("y");
				var c = elem.getAttribute("i");
				elem.innerHTML = '<iframe referrerpolicy="no-referrer-when-downgrade" width="' + w + '" height="' + parseInt(h) + '" src="//www.standout.com.br/' + c + '/p/' + p + '" frameborder="0" id="frameStandout" allowfullscreen></iframe>';

				if (elem.getAttribute("x") == "landing-page") {
					//Adiciona Scrolling "No" na DIV de iframe da Standout
					var elemIframeNoScroll = document.getElementById("frameStandout");
					elemIframeNoScroll.setAttribute("scrolling", "no");
				}
			}
		}
		sessionStorage.setItem('StandoutSession', '');
		sessionStorage.setItem('StandoutUrl', '');
	}
}

//MENSAGERIA
if (document.getElementById('frameStandout') != null || document.getElementById('frameStandout') != 'undefined') {

	standoutMensageria();

	function standoutMensageria() {
		var myMensageriaVitrine = document.getElementById('frameStandout');
		var myMensageriaOrigin = '*';
		//var myMensageriaHeight = document.getElementById("frameStandout").height;
		console.log("MSG 2.0 - JS");

		// Listen for messages
		if (window.addEventListener) {
			window.addEventListener('message', onMessageReceived, false);
		}
		else {
			window.attachEvent('onmessage', onMessageReceived, false);
		}

		// Handle messages received from origin only
		function onMessageReceived(event) {
			//console.log("origin: "+event.origin);
			if ((event.origin == "https://www.drsystems.com.br") || (event.origin == "https://www.standout.com.br")) {
				//Se origem for as esperadas, continue...
				//console.log("Origem Valida");
				//console.log("origin: "+event.origin);
			}
			else {
				//Se origem NAO for as esperadas, PARE...
				//console.log("Origem Invalida");
				return false;
			}

			if (myMensageriaOrigin === '*') {
				myMensageriaOrigin = event.origin;
			}

			if (event.data.stdToken) {
				// console.log('eventJS', event);
				// console.log("originJS: "+event.origin);

				if (event.data.stdToken == codigoEmbed) {
					var myMensageriaVitrine = document.getElementById('frameStandout');
					
					if ((window.location.href.indexOf("/caudalie/") > -1) ) {
						getPrice();
					}

					if (event.data.method == "getMensageriaAccordion") {
						// console.log("JS getMensageriaAccordion: "+event.data.value);
						// console.log(event.data.value);
						console.log("JS getMensageriaAccordionALTURA: " + event.data.value.alturaInicial);
						console.log("JS getMensageriaAccordionPOSICAO: " + event.data.value.posicaoAtual);

						if (parseInt(window.innerWidth) <= 420) {
							//console.log('mobile');
							myMensageriaVitrine.setAttribute('height', parseInt(event.data.value.alturaInicial + 80));
							myMensageriaVitrine.setAttribute('style', 'height:' + parseInt(event.data.value.alturaInicial + 80) + 'px;');

							window.scrollTo({
								'behavior': 'smooth',
								'left': 0,
								'top': event.data.value.posicaoAtual + 56
							});

						} else {
							//console.log('desktop');
							myMensageriaVitrine.setAttribute('height', event.data.value.alturaInicial);
							myMensageriaVitrine.setAttribute('style', 'height:' + event.data.value.alturaInicial + 'px;');

							window.scrollTo({
								'behavior': 'smooth',
								'left': 0,
								'top': event.data.value.posicaoAtual + 50
							});
						}

					}

					if (event.data.method == "getMensageriaFirstHeight") {
						console.log("JS getMensageriaFirstHeight: " + event.data.value);
						if(event.data.value <= 20) {
							if(document.querySelector("#standoutDivAutomatico")){
								event.data.value = document.querySelector("div#standoutDiv").getAttribute("h");
							} else {
								event.data.value = 700;
							}
							console.log("JS getMensageriaFirstHeight reset: "+event.data.value);
						}
						myMensageriaVitrine.setAttribute('height', event.data.value);
						myMensageriaVitrine.setAttribute('style', 'height:' + event.data.value + 'px;');
					}

					if (event.data.method == "getMensageriaHeight") {
						//console.log("getHeight: "+event.data.value);
						myMensageriaVitrine.setAttribute('height', event.data.value);
						myMensageriaVitrine.setAttribute('style', 'height:' + event.data.value + 'px;');
					}

					if (event.data.method == "getMensageriaMobileHeight") {
						//console.log("getMobileHeight: "+event.data.value);
						myMensageriaVitrine.setAttribute('height', parseInt(event.data.value + 20));
						myMensageriaVitrine.setAttribute('style', 'height:' + parseInt(event.data.value + 20) + 'px;');

						//faz smooth scroll (top)
						var style = document.createElement('style');
						style.innerHTML = 'html { scroll-behavior: smooth; }';

						var ref = document.querySelector('script');
						ref.parentNode.insertBefore(style, ref);

						// window.scrollTo({
						//  'behavior': 'smooth',
						//   'left': 0,
						//  'top': myMensageriaVitrine.offsetTop - 150
						// });
						document.getElementById("standoutDivAutomatico").scrollIntoView({ block: "start", behavior: "smooth" });
					}
					
					if (event.data.method == "getMensageriaPromo") {
						console.log("JS getMensageriaPromo: " + event.data.value);
						myMensageriaVitrine.setAttribute('height', event.data.value);
						myMensageriaVitrine.setAttribute('style', 'height:' + event.data.value + 'px;');
					}

					if (event.data.method == "mensageriaScrollMenuGoTo") {
						console.log("JS mensageriaScrollMenuGoTo: " + event.data.value);
						
						//Tratamento específico para posicionar o conteúdo após o clique do menu,
						//adicionando height adicional dos itens da página da marca
						var extraHeightLP = 0;
						if (window.location.href.indexOf("sephora.com.br/caudalie/") >= 0) {

							var bcr__content = document.querySelector(".bcr__content");
							if (bcr__content) {
								extraHeightLP = bcr__content.offsetTop;
								console.log('extraHeightLP2', extraHeightLP);
							}
						}

						window.scrollTo({
							'behavior': 'smooth',
							'left': 0,
							'top': event.data.value + extraHeightLP - 100
						});
					}
				}
			}
		}
	}
}

//categoria com preco
function getPrice() {
	//setTimeout(function () {
		if ((window.location.href.indexOf("/caudalie/") > -1) ) {
			if (document.getElementById('frameStandout') != null || document.getElementById('frameStandout') != 'undefined') {
				var myMensageriaVitrine = document.getElementById('frameStandout');
				
				var blockProd = [];
				
				if(document.querySelectorAll("div.chaordic-container iframe").length > 1) {
					var arrProdutos = [];
					var arrProdutosLen = 0;
					for (f = 0; f < document.querySelectorAll("div.chaordic-container iframe").length; f++) {
						
						if ((document.querySelectorAll("div.chaordic-container iframe")[f].contentDocument.body.querySelectorAll("div.carousel-list ul.carousel-products li.carousel-item").length > 0) ) {
							var blockProd = document.querySelectorAll("div.chaordic iframe")[f].contentDocument.body.querySelectorAll("div.carousel-list ul.carousel-products li.carousel-item");
						}
						
						if (blockProd.length > 0) {
							for (b = 0; b < blockProd.length; b++) {
								if (blockProd[b] === 'undefined') {
									//undefined
								} else {
									var preco = 0;
									var oldPreco = 0;
									if (blockProd[b].querySelector("div.prices a") != undefined) {
										//console.log('Price: ',blockProd[b].querySelector("div.product-price div.price-box .regular-price"));
										if (blockProd[b].querySelector("div.prices a") != null) {
											//console.log('Price regular: ',blockProd[b].querySelector("div.product-price div.price-box span .regular-price span:nth-child(2)"));
											//preco = blockProd[b].querySelector("div.prices a").innerText.trim().replace('R$ ', '');
											preco = blockProd[b].querySelector("div.prices a").innerHTML.replaceAll('\n','').trim().replace('R$','').replace('&nbsp;','');
										}

										/*
										if (blockProd[b].querySelector("div.content div.prices a.old-price") != null) {
											//console.log('Price regular: ',blockProd[b].querySelector("div.product-price div.price-box span .regular-price span:nth-child(2)"));
											oldPreco = blockProd[b].querySelector("div.content div.prices a.old-price").textContent.trim().replace('R$ ', '');
										}
										*/
									}
									if (blockProd[b].getAttribute("data-productid") != undefined) {
										var produtoId = blockProd[b].getAttribute("data-productid");
									} else {
										var produtoId = 0;
									}
									if (blockProd[b].getAttribute("data-productid") != undefined) {
										var produtoCodigo = blockProd[b].getAttribute("data-productid");
									} else {
										var produtoCodigo = 0;
									}
									if (blockProd[b].querySelector("div.content a").href != undefined) {
										var produtoUrl = blockProd[b].querySelector("div.content a").href;
										var produtoNome = blockProd[b].querySelector("div.content a.product-name").innerText.trim();
									} else {
										var produtoUrl = "";
										var produtoNome = "";
									}
									
									var produtoQty = 0;
									
									var produtoPreco = preco;
									var produtoOldPreco = oldPreco;
									var produtoDesconto = '';

									//monta array/json
									arrProdutos[arrProdutosLen] = ['{"produtoId":"' + produtoId + '","produtoCodigo":"' + produtoCodigo + '","produtoQty":"' + produtoQty + '","produtoNome":"' + produtoNome + '","produtoUrl":"' + produtoUrl + '","produtoPreco":"' + produtoPreco + '","produtoOldPreco":"' + produtoOldPreco + '","produtoDesconto":"' + produtoDesconto + '"}'];
									console.log('---', arrProdutos[arrProdutosLen]);
									arrProdutosLen = arrProdutos.length+1;
								}
							}
						}
					}
					
					//console.log('STANDOUT arrProdutos: ',arrProdutos.filter(subArray => subArray.length > 0));
					var stringJson = arrProdutos.filter(subArray => subArray.length > 0).toString();
					console.log('STANDOUT JSON: ',stringJson);
					//enviar json via postmessage para standout
					
					var message = { "method": "getPriceSephora", "value": stringJson };
					//console.log("msg json", message);
					myMensageriaVitrine.contentWindow.postMessage(message, "*");

					//aumenta a altura do frame
					myMensageriaVitrine.setAttribute('height', parseInt(document.getElementById('frameStandout').height) + 50);
					myMensageriaVitrine.setAttribute('style', 'height:' + parseInt(parseInt(document.getElementById('frameStandout').height) + 50) + 'px;');
					
				}
			}
		}
	//}, 1000);
}


function catchProductData(){

	var dateNewStd = new Date();
	dateNewStd.setSeconds(0);

	if(sessionStorage.getItem('StandoutSessionCPD') == 'true' && sessionStorage.getItem('StandoutUrlCPD') == window.location.href && sessionStorage.getItem('StandoutDateCPD') == dateNewStd ){
		console.log('StandoutJSInitCPD - Chamada CPD duplicada');
		//libera session
		// sessionStorage.setItem('StandoutSessionCPD', '');
		// sessionStorage.setItem('StandoutUrlCPD', '');
		
	} else {
		// console.log('StandoutJSInitCPD - Chamada CPD');
		sessionStorage.setItem('StandoutSessionCPD', 'true');
		sessionStorage.setItem('StandoutUrlCPD', window.location.href);
		
		var dateStd = new Date();
		dateStd.setSeconds(0);
		sessionStorage.setItem('StandoutDateCPD', dateStd);
		
		setTimeout(function () {
			// console.log("CPD location",window.location);
			if (window.location.href.indexOf("busca") >= 0 || window.location.href.indexOf("search") >= 0) {
				//nao executa
			} else {
				console.log("--- CPD INIT ---");
				var validaCPD = 1;

				var skuCPD = getEan();
				var precoCPD = getRegularPrice();
				var fullPrice = getFullPrice();
				var disponibilidadeCPD = getAvailability();
				var precoBeneficioCPD = getPriceBenefit();
				var PidCPD = getProdId();
				var SellerCPD = getSeller();
				var TituloPd = getTitle();
				var DescricaoHtmlPd = getDescriptionHtml();
				var DescricaoTextPd = getDescriptionText();
				var imgDefaultPD = getImageDefault();
				var imgsPD = getImagesGroup();
				
				var url = window.location.href;
				var urlNew = url.replace("/#/", "/");

				if(validaCPD){
					setTimeout(function () {
						var dataPd = "distributor="+distributor+"&sku="+skuCPD+"&url="+encodeURIComponent(urlNew)+"&preco="+precoCPD+"&preco_beneficio="+precoBeneficioCPD+"&product_id_distributor="+PidCPD+"&seller="+SellerCPD+"&disponibilidade="+disponibilidadeCPD+"&TituloPd="+TituloPd+"&imgDefaultPD="+imgDefaultPD+"&imgsPD="+imgsPD.toString()+"&DescricaoTextPd="+encodeURIComponent(DescricaoTextPd)+"&DescricaoHtmlPd="+encodeURIComponent(DescricaoHtmlPd)+"&preco_sem_desconto="+fullPrice;
						//console.log('dataPd', dataPd);
		
						var urlCatchProductData = 'https://www.standout.com.br/'+distributor+'/catchProductData.php';
						var paramsCatchProductData = dataPd;
						
						var xmlhttpCPD = new XMLHttpRequest();
						
						xmlhttpCPD.addEventListener("readystatechange", function() {
							if(this.readyState === 4 && this.status === 200) {
								console.log('STD-CPD => True');
								// if (this.responseText != '') {
								// 	var myObjCPD = JSON.parse(this.responseText);
								// 	console.log('STD-CPD => True', myObjCPD);
								// } else {
								// 	console.log('STD-CPD => True', skuCPD);
								// }
							} 							 
						});
						
						xmlhttpCPD.open("POST", urlCatchProductData, true);
						xmlhttpCPD.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
						xmlhttpCPD.send(paramsCatchProductData);
						
					}, 1000);
				} else {
					console.log('STD-CPD => False');
				}
			}
		}, 1000);
	}
}


/*	**************************************************	*/
/*								Function PADRÃO											  */
/*	**************************************************	*/

function getEan(){
	var ean = '';
	try {
		var varejoEANRef = document.querySelector("input[name='EAN-Code']");
		if (varejoEANRef) {
			var varejoEANRefDATA = varejoEANRef.value;
			if (varejoEANRefDATA) {
				ean = varejoEANRefDATA;
			}
		}		
	} catch (error) {}
	return ean;
}

function getRegularPrice(){
	var preco = 0;
	try {
		var varejoPrecoRef = document.querySelectorAll(".product-price .price-box .price-sales span");
		if (varejoPrecoRef.length > 0) {
			preco = convertPrice(varejoPrecoRef[0].innerText)
		} 
	} catch (error) {}
	return preco;
}

function getFullPrice(){
	var fullPrice = 0;
	try {
		var fullPriceRef = document.querySelector('.product-cart__princing .price-box .price-standard')

		if(fullPriceRef){
			fullPrice = convertPrice(fullPriceRef.textContent)
		} else {
			fullPrice = getRegularPrice()
		}
	} catch (error) {}
	return fullPrice;
}

function getAvailability(){
	var disponibilidade = 0;
	try {
		var varejoDisponibilidadeRef = document.querySelectorAll(".product-add-to-cart button#add-to-cart");

		if (varejoDisponibilidadeRef.length > 0) {
			var btnDisabled = varejoDisponibilidadeRef[0].getAttribute("disabled");

			if (btnDisabled) {
				disponibilidade = 0;
			} else {
				disponibilidade = 1;
			}
		}
	} catch (error) {}
	return disponibilidade;
}

function getPriceBenefit(){
	var precoBeneficio = 0;
	try {
		
	} catch (error) {}
	return precoBeneficio;
}

function getProdId(){
	var prodId = '';
	try {
		
	} catch (error) {}
	return prodId;
}

function getSeller(){
	var seller = '';
	return seller;
}

function getTitle(){
	var titulo = '';
	try {
		var tituloRef = document.querySelector('h1.product-name');

		if(tituloRef){
			titulo = tituloRef.textContent
		}
	} catch (error) {}
	return titulo;
}

function getDescriptionText(){
	var descricaoText = '';
	try {
		var descRef = document.querySelector('.product-description__text')

		if(descRef){
			descricaoText = descRef.textContent.trim()
		}
	} catch (error) {}
	return descricaoText;
}

function getDescriptionHtml(){
	var descricaoHtml = '';
	try {
		var descRef = document.querySelector('.product-description__text')

		if(descRef){
			descricaoHtml = descRef.innerHTML.trim()
		}
	} catch (error) {}
	return descricaoHtml;
}

function getImageDefault(){
	var imgPrincipal = '';
	try {
		var imgRef = document.querySelectorAll('.product-thumbnails li img');

		if(imgRef.length > 0){
			imgPrincipal = imgRef[0].src.replaceAll('&',encodeURIComponent('&'));
		}
	} catch (error) {}
	return imgPrincipal;
}

function getImagesGroup(){
	var imgsProduto = [];
	try {
		var imgsGroupRef = document.querySelectorAll('.product-thumbnails li img');
		if(imgsGroupRef.length > 0){
			imgsGroupRef.forEach(image => {
				imgsProduto.push(image.src.replaceAll('&',encodeURIComponent('&')))
			})
		} else {
			imgsProduto[0] = getImageDefault();
		}
	} catch (error) {}
	return imgsProduto;
}

/*	**************************************************	*/
/*								Function AUXILIARES											  */
/*	**************************************************	*/

function convertPrice(originalPrice){
	var hasDecimal = /[\.,]\d{2}$/.test(originalPrice);

	if(hasDecimal){
		return Number(originalPrice.replace(/[^0-9-]+/g,""))/100;	
	} else {
		return Number(originalPrice.replace(/[^0-9-]+/g,""));	
	}
}


function extractDigits(input) {
	const numberExtractorRegex = /\d+/;
	const match = input.match(numberExtractorRegex);
	return match ? match[0] : 0;
}