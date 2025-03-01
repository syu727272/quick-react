# コーディング規約

## 1. 基本原則

- DRY (Don't Repeat Yourself) 原則に従う
- KISS (Keep It Simple, Stupid) を心がける
- 可読性を最優先する
- コンポーネントは単一責任の原則に従う

## 2. 命名規則

### 2.1 ファイル名

- コンポーネント: パスカルケース (`Button.jsx`, `UserProfile.jsx`)
- ユーティリティ/フック: キャメルケース (`useAuth.js`, `formatDate.js`)
- スタイル: コンポーネント名に `.module.css` または `.module.scss` を付加

### 2.2 変数/関数名

- 変数名: キャメルケース、説明的な名前を使用
- ブール値: `is`, `has`, `should` などの接頭辞を使用
- イベントハンドラ: `handle` + イベント名 (`handleClick`, `handleSubmit`)
- コールバック関数: `on` + イベント名 (`onClick`, `onSubmit`)

## 3. コンポーネント構造

```jsx
import React from 'react';
import PropTypes from 'prop-types';
import styles from './Component.module.css';

// 定数は上部に定義
const MAX_ITEMS = 10;

// 関数コンポーネントを使用
function Component({ prop1, prop2 }) {
  // ステート、エフェクトを先に定義
  const [state, setState] = useState(initialState);
  
  // イベントハンドラ
  const handleClick = () => {
    // 処理
  };
  
  // ヘルパー関数
  const helperFunction = () => {
    // 処理
  };
  
  // 早期リターン
  if (!prop1) return null;
  
  // JSXを返却
  return (
    <div className={styles.container}>
      {/* 内容 */}
    </div>
  );
}

// PropTypes の定義
Component.propTypes = {
  prop1: PropTypes.string.isRequired,
  prop2: PropTypes.number,
};

// デフォルトプロップ
Component.defaultProps = {
  prop2: 0,
};

export default Component;
```

## 4. ESLint 設定

```javascript
module.exports = {
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'plugin:jsx-a11y/recommended',
    'prettier'
  ],
  plugins: ['react', 'react-hooks', 'jsx-a11y'],
  rules: {
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'error',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
    'no-unused-vars': 'warn',
  },
  parserOptions: {
    ecmaVersion: 2021,
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true
    }
  },
  settings: {
    react: {
      version: 'detect'
    }
  }
};
```

## 5. Prettier 設定

```json
{
  "singleQuote": true,
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "printWidth": 100,
  "bracketSpacing": true,
  "endOfLine": "lf"
}
```