# constraint布局使用

+ 基本属性```layout_constraintXXX1_toXXX2=id```，view的xxx1属性值设为id的xxx2属性值

  - layout_constraintBaseline_toBaselineOf （View A 内部文字与 View B 内部文字对齐）
  - layout_constraintLeft_toLeftOf （View A 与 View B 左对齐）
  - layout_constraintLeft_toRightOf （View A 的左边置于 View B 的右边）
  - layout_constraintRight_toLeftOf （View A 的右边置于 View B 的左边）
  - layout_constraintRight_toRightOf
  - layout_constraintTop_toTopOf
  - layout_constraintTop_toBottomOf
  - layout_constraintBottom_toTopOf
  - layout_constraintBottom_toBottomOf
  - layout_constraintStart_toEndOf
  - layout_constraintStart_toStartOf
  - layout_constraintEnd_toStartOf
  - layout_constraintEnd_toEndOf

  如：

  ```xml
      <Button
          android:text="Source"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          app:layout_constraintRight_toLeftOf="@id/target"
          app:layout_constraintBottom_toTopOf="@id/target"/>
  ```

  button的Right就等于id是target view的right属性

  button的Bottom属性就等于target view的top属性

  显示效果就是button在target的左上方

  ![效果图](H:\Typora\image\constraint1.png)

每个constraint内的view都应该指定水平、垂直约束，