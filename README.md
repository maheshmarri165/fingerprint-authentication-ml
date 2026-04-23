# fingerprint-authentication-ml
#Evaluation Metrics (Security Metrics)
from sklearn.metrics import confusion_matrix

def evaluate_model(y_true, y_pred):

    tn, fp, fn, tp = confusion_matrix(y_true, y_pred).ravel()

    accuracy = (tp + tn) / (tp + tn + fp + fn)

    FAR = fp / (fp + tn)
    FRR = fn / (fn + tp)

    precision = tp / (tp + fp)
    recall = tp / (tp + fn)

    print("Accuracy:", round(accuracy,4))
    print("FAR:", round(FAR,4))
    print("FRR:", round(FRR,4))
    print("Precision:", round(precision,4))
    print("Recall:", round(recall,4))

    return accuracy, FAR, FRR

cnn_pred_prob = cnn_model.predict(val_generator)

cnn_pred = (cnn_pred_prob > 0.5).astype(int)
y_true_cnn = val_generator.classes
print("CNN Results")
cnn_acc, cnn_far, cnn_frr = evaluate_model(y_true_cnn, cnn_pred)
hybrid_pred_prob = hybrid_model.predict(val_generator)

hybrid_pred = (hybrid_pred_prob > 0.5).astype(int)
print("Hybrid CNN Results")
hybrid_acc, hybrid_far, hybrid_frr = evaluate_model(y_true_cnn, hybrid_pred)

svm_pred = svm.predict(X_test)
print("SVM Results")

svm_acc, svm_far, svm_frr = evaluate_model(y_test, svm_pred)

rf_pred = rf.predict(X_test)
print("\nRandom Forest Results")

rf_acc, rf_far, rf_frr = evaluate_model(y_test, rf_pred)
