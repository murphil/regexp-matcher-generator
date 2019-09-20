```js
const uCase =
    [ '~/plugins/TsVue'
    , '~sadf-x'
    , '@xxx'
    , 'asdf'
    ]

const externalModules = {
    saasTsVue: '1.2.3'
}

const manifest = {
    '^~/plugins/TsVue$' (name, m, ms) {
        return 'saasTsVue.' + ms['saasTsVue']
    },
    '^[~@]\(.*\)' (name, m, ms) {
        return m[1] + '.' + (ms[m[1]] || '0.0.0')
    },
    '.*' (name, m, ms) {
        return `${name}.0.0.0`
    }
}

const matcher = matchRegexp(manifest)

uCase.forEach(name => {
    let r = matcher(name, externalModules)
    console.log(r)
}) /*
saasTsVue.1.2.3
sadf-x.0.0.0
xxx.0.0.0
asdf.0.0.0
*/
```