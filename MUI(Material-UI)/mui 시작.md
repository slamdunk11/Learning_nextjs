# 1. mui 설치
```
// with npm
npm install @mui/material @emotion/react @emotion/styled

// with yarn
yarn add @mui/material @emotion/react @emotion/styled
```


```
// with npm
npm install @mui/icons-material

// with yarn
yarn add @mui/icons-material
```

> `yarn add @mui/material @emotion/react @emotion/styled` 이걸로 안 하고 다른? 걸로 하니까    
> `Module not found: Can't resolve '@mui/material/utils'` 이런 에러가 뜸   
> 해결 방법도 `npm install @mui/material @emotion/react @emotion/styled` 이걸 하는 거였음(첨부터 잘 설치하자!)

# 2. mui 사용법
```javascript
import { AppBar, Box, IconButton, styled, TextField, Toolbar } from '@material-ui/core'
import { DesktopWindows as DesktopIcon, PhoneIphone as PhoneIcon } from '@mui/icons-material'
// as를 사용해서 이름 바꿔주기 가능
...

      <Box>
        <AppBar>
          <Toolbar>
            <TextField></TextField>
            <Box>
             <DeviceButton>
               <PhoneIcon />
             </DeviceButton>
             <DeviceButton>
               <DesktopIcon />
             </DeviceButton>
            </Box>
          </Toolbar>
        </AppBar>
      </Box>
```
