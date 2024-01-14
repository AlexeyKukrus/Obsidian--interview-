**ОТВЕТ:
	В Webpack плагины (plugins) и загрузчики (loaders) играют разные роли в обработке и сборке файлов.
	- Загрузчики (loaders) - это модули, которые позволяют обрабатывать и преобразовывать файлы во время сборки. Примеры загрузчиков в Webpack: babel-loader, css-loader, file-loader, sass-loader
	- Плагины (plugins) - это модули, которые добавляют дополнительную функциональность или выполняют определенные задачи во время сборки проекта. Они могут влиять на работу компилятора Webpack и предоставлять функциональность, которая не может быть достигнута только с использованием загрузчиков. Примеры плагинов в Webpack: HtmlWebpackPlugin, MiniCssExtractPlugin, DefinePlugin, CopyWebpackPlugin.**

Плагины (plugins) в Webpack - это дополнительные модули, которые расширяют функциональность компилятора Webpack и позволяют выполнять различные задачи во время сборки проекта. Они представляют собой специальные объекты, которые конфигурируются и добавляются в настройки сборки
```javascript
//webpack.config.js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = (env) => {
	return {
		mode: env.mode ?? 'development',
		entry: path.resolve(__dirname, 'src', 'index.js'),
		output: {
			path: path.resolve(__dirname, 'build'),
			filename: '[name].[contenthash].js',
			clean: true
		},
		plugins: [
			new HtmlWebpackPlugin({ template: path.resolve(__dirname, 'public', 'index.html')})
		],
	}
};