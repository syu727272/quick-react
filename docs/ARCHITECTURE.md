## 4. アーキテクチャ設計書

```markdown
# アーキテクチャ設計書

## 1. 概要

QuickReact は、モダンな React アプリケーションのベストプラクティスに従って設計されています。このドキュメントでは、アプリケーションの構造、データフロー、状態管理などの基本的な設計原則について説明します。

## 2. アプリケーション構造

### 2.1 ディレクトリ構造

## 3. データフロー

### 3.1 基本的なデータフロー

QuickReact は主に単方向データフローを採用しています：

1. 状態（state）はコンポーネント内、またはコンテキストで管理
2. 親コンポーネントから子コンポーネントへは props を通じてデータを渡す
3. 子コンポーネントから親コンポーネントへは、コールバック関数を通じてイベントを通知
4. 状態の更新は常に上位のコンポーネントまたはコンテキストで行う

## 3. 技術スタック

- **フロントエンド**: React 18、React Router v6
- **状態管理**: React Context API + useReducer
- **スタイリング**: CSS Modules + SASS
- **テスト**: Jest + React Testing Library
- **ビルド/開発ツール**: Create React App、ESLint、Prettier
- **パフォーマンス計測**: Web Vitals

## 4. コンポーネント設計原則

### 4.1 コンポーネント階層

- **ページコンポーネント**: ルートレベルのコンポーネント、ルーティングに対応
- **コンテナコンポーネント**: データ取得とビジネスロジックを担当
- **プレゼンテーショナルコンポーネント**: UIの表示のみを担当、主に props を受け取る

### 4.2 コンポーネントの責務分離

- **関心の分離**: UIとデータ取得ロジックを分離する
- **単一責任の原則**: 各コンポーネントは1つのことだけを行う
- **再利用可能なコンポーネント**: 汎用性の高いコンポーネントは再利用できるように設計
- **関連するコンポーネントは同じフォルダにまとめる**

### 4.3 コンポーネント命名規則

- ファイル名とコンポーネント名は一致させる
- コンポーネントは PascalCase で名前付け

## 5. データフロー

### 5.1 状態管理アーキテクチャ

QuickReactではReact Context APIとuseReducerを組み合わせた軽量な状態管理を採用します。

### 5.2 グローバル状態と局所状態

- **局所状態**: 特定のコンポーネントまたは機能に限定された状態
- **グローバル状態**: アプリケーション全体で共有される状態（ユーザーセッション、テーマ設定など）

### 5.3 非同期データフローパターン

API呼び出しなどの非同期操作は以下のパターンで処理します：

1. **ローディング状態の管理**
   ```javascript
   // hooks/useDataFetching.js
   export function useDataFetching(fetchFunction) {
     const [isLoading, setIsLoading] = useState(false);
     const [data, setData] = useState(null);
     const [error, setError] = useState(null);
     
     const execute = async (...args) => {
       setIsLoading(true);
       try {
         const result = await fetchFunction(...args);
         setData(result);
         return result;
       } catch (err) {
         setError(err);
         throw err;
       } finally {
         setIsLoading(false);
       }
     };
     
     return { isLoading, data, error, execute };
   }
   ```

## 6. ルーティング

React Router v6を使用して、宣言的なルーティングを実装します：

```javascript
<Routes>
  <Route path="/" element={<HomePage />} />
  <Route path="/about" element={<AboutPage />} />
  <Route path="/dashboard" element={
    <ProtectedRoute>
      <DashboardPage />
    </ProtectedRoute>
  } />
  <Route path="*" element={<NotFoundPage />} />
</Routes>