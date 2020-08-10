# EasyRecyclerView

This class will help you create a list view with `RecyclerView` class more easily.

## Install via gradle using "jitpack.io"

In your root-level "build.gradle" file, put:
```
    allprojects {
        repositories {
            jcenter()
            maven { url "https://jitpack.io" }
        }
   }
```

In your app-level "build.gradle" file, put:
```
   dependencies {
        implementation 'com.github.PerrchicK:EasyRecyclerView:0.0.1'
   }
```

# Usage

As it appears [here (you may take this example code as well)](https://github.com/PerrchicK/android-app/blob/58bd56e97a29aa912a151601bb7a71e1450d2d3b/app/src/main/java/com/perrchick/someapplication/uiexercises/list/EasyListActivity.java#L28) you can adopt EasyRecyclerView programmatically by adding its view to some parent.
```java
public class EasyListActivity extends AppCompatActivity {

    private ArrayList<SomePojo> list;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_easy_list);

        ViewGroup mainLayout = findViewById(R.id.main_layout);
        list = new ArrayList<>();
        EasyRecyclerView<SomePojo> easyRecyclerView = new EasyRecyclerView<>(this, new EasyRecyclerView.CellsFactory<SomePojo>() {
            @Override
            public EasyRecyclerView.CellHolder<SomePojo> create(ViewGroup parent, int viewType) {
                // Please read: https://possiblemobile.com/2013/05/layout-inflation-as-intended/
                View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.list_row, null);
                return new Cell(view);
            }
        });

        for (int i = 0; i < 1000; i++) {
            SomePojo obj = new SomePojo();
            obj.setName("obj" + i);
            list.add(obj);
        }

        mainLayout.addView(easyRecyclerView, new ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
        easyRecyclerView.setData(list);
    }

    private class Cell extends EasyRecyclerView.CellHolder<SomePojo> {
        private final TextView textView;

        public Cell(View itemView) {
            super(itemView);
            textView = (TextView) itemView.findViewById(R.id.text_view);
        }

        @Override
        public void configure(SomePojo data) {
            super.configure(data);
            textView.setText(data.getName());
        }

        @Override
        public void prepareForReuse() {
            textView.setText("");
        }
    }
}
```
